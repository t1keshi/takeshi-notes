# Visual Studio Code

settings.json

É o arquivo de configurações do VS Code, em formato JSON (aceita comentários, por isso jsonc). Cada chave é uma configuração, e o valor define o comportamento. Esse é o arquivo de usuário, que vale para todos os projetos. Um .vscode/settings.json dentro da pasta do projeto vale só para aquele projeto.

# Como integrar um terminal no VS Code

Por exemplo, para utilizar o terminal **x64 Native Tool Commands Prompt for VS 2022** no VS Code, basta adicionar os parâmetros abaixo em ```settings.json```.

```json
    "terminal.integrated.profiles.windows": {
        "Nome do seu PowerShell": {
            "path": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
            "args": [
                "-NoExit",
                "-Command",
                "& { Import-Module 'C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\Common7\\Tools\\Microsoft.VisualStudio.DevShell.dll'; Enter-VsDevShell -VsInstallPath 'C:\\Program Files\\Microsoft Visual Studio\\2022\\Community' -SkipAutomaticLocation -DevCmdArguments '-arch=x64' }"
            ]
        }
    },
    "terminal.integrated.defaultProfile.windows": "Nome do seu PowerShell"
```

```terminal.integrated.profiles.windows```

Define a lista de perfis de terminal disponíveis ao clicar em ```+``` em ```Terminal```. Cada perfil tem um nome (por exemplo: ```"MSVC x64 PowerShell"```) e um objeto com as opções de como iniciar o shell.

```path```

O executável que será iniciado: o Windows PowerShell 5.1. As barras são duplicadas (\\) porque a barra invertida é caractere de escape em JSON. Para usar o PowerShell 7, o caminho seria o pwsh.exe.

```args```

A lista de argumentos passados ao executar o terminal (neste caso, **powershell.exe**).

- ```-NoExit```: mantém o terminal aberto depois de executar o comando. Sem ele, o PowerShell rodaria o comando e fecharia na hora.
- ```-Command```: diz ao PowerShell que o próximo argumento é um comando a executar na inicialização.

O texto do comando:

```& { ... }```: o operador de chamada ```&``` executa o bloco ```{ ... }``` num escopo próprio. Serve só para agrupar os dois comandos internos.

```Import-Module '...DevShell.dll'```: carrega o módulo do Visual Studio que contém o cmdlet ```Enter-VsDevShell```. Sem isso, o PowerShell não conhece esse comando.

O operador ```;``` separa os cmandos que rodam em sequência.

```Enter-VsDevShell```: o cmdlet que configura o ambiente de desenvolvimento do MSVC. Ele ajusta PATH, INCLUDE, LIB e outras variáveis, e é isso que faz o ```cl``` ser encontrado.

```-VsInstallPath '...\Community'```: a pasta de instalação do Visual Studio para que cmdlet ```Enter-VsDevShell``` consiga encontrar o Visual Studio.

```-SkipAutomaticLocation```: impede que ele mude o diretório atual para a pasta do usuário. Assim o terminal mantem o diretorio do projeto aberto no VSCode.

```-DevCmdArguments '-arch=x64'```: argumentos repassados ao VsDevCmd.bat interno. ```-arch=x64``` faz o compilador gerar código de 64 bits. Para 32 bits seria ```-arch=x86```. Existe também ```-host_arch=x64```, que escolhe o compilador nativo de 64 bits (mais rápido).

As aspas simples ```'...'``` dentro do JSON evitam ter de escapar aspas duplas, e o PowerShell trata o conteúdo como texto literal.