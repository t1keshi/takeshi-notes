Previous: [Game Development](game_dev.md)  


# Multiplayer Game Development

In a client-server model, players all connect to a central server, whereas in a peer-to-peer model, every player connects to every other player.

A peer-to-peer model requires O(n2) bandwidth. This means that the bandwidth grows at a quadratic rate based on the number of users. In this case, with n being as high as 128, using peer-to-peer would lead to very little bandwidth per player.

In client-server model, the bandwidth requirements of each player remain constant, while the server must handle only O(n) bandwidth. However, this meant that the server needed to be on a network that would allow for several incoming connections—the type of connection. 


# Evolution of multiplayer games  

Os primeiros jogos multijogadores locais foram _Tennis for Two_ (1958) e _Spacewar!_ (1962) onde dois ou mais jogadores jogavam o jogo em um único computador.  

Os primeiros jogos multijogadores em rede surgiram na plataforma PLATO onde os jogos se comunicavam através de dois ou mais mainframes conectados em rede. Os jogos pioneiros desta época foram _Empire_ (1973) e _Maze War_ (1973).

Em 1970, no início da popularização de computadores pessoais (PC), uma das maneiras de dois computadores se comunicarem era através de portas serial. Entretanto, cada PC possuia poucas portas serial. Para que múltiplos PC pudessem se conectar foi criado o esquema **daisy chain** - uma topologia de rede em forma de anel.

Em 1978, Rob Trushaw criou o jogo MUD (Multi-User Dungeon) onde diversos jogadores se conectavam em um mundo virtual persistente. Este gênero de jogo ganhou muita popularidade em mainframes de universidades.

Com o surgimento de modem, dois computadores podiam se conectar através de linhas telefônicas. Apesar da transmissão de dados ser extretamente lenta, foi com esta tecnologia que os jogadores puderam jogar MUD fora das universidades.

Local Area Network (LAN) é um termo utilizado para descrever computadores conectados em rede em uma pequena área. Com o surgimento de Ethernet, LAN se tornou extremamente popular. O jogo _Doom_ (1993) foi o percursor em muitas áreas relacionadas ao desenvolvimento de jogos. Até hoje, a arquitetura de jogos em rede modernos são inspirados por conceito chaves introduzidos pelo _Doom_.


Muitos jogos multijogadores em rede que tinham suporte a LAN ajudaram a popularizar um fenômeno conhecido como LAN-parties onde os jogadores se reuniam em algum espaço e conectavam seus computadores em rede para jogar. Hoje os jogos tem abandonado suporte a LAN e mantendo apenas o modo online.

Um jogo online conectam jogadores que estão fisicamente distantes através de uma rede global. Com o advento da Internet em 1990, os jogos mais populares desta época foram _Quake_ (1996) e _Unreal_ (1998).

A principal consideração entre jogos online e jogos em LAN é a latência - o tempo gasto para que um pacote de dados viage de um computador para outro.

Jogos online chegaram nos consoles nos anos 2000 com Xbox Live e Playstation Network (serviços que baseados em serviços para PC como GameSpy e DWANGO).

Alguns jogos multijogadores em rede tem um limite para o número de jogadores, por exemplo, de 4 a 32 jogadores. Entretanto, o gênero de jogo MMO (Massive Multiplayer Online) permite que milhares de jogadores joguem o jogo simultaneamente em um mesmo mundo persistente. De muitas maneiras, MMO pode ser pensado como uma evolução dos jogos do gênero MUD. Um dos primeiros jogos do gênero MMO foi _Habitat_ (1986) que utiliza serviços como Quantum Link e CompuServe para acesso a rede. Os primeiros jogos MMO que se tornaram populares e obtiveram sucesso foram _Ultima Online_ (1997), _EverQuest_ (1999) e _World of Warcraft_ (2004). 


# Networking model in FPS

- support to 128 players  
- support to LAN or Internet  
- latency consideration  
- speed consideration  
- communication protocol: unreliable
- different types of data transmission (non-guaranteed data, guaranteed data, most recente state data, guaranteed quickest data)  
- client-server model  
- networking implementation into several different layers: platform packet module

platform packet module

A packet is a formatted set of data sent over a network. It is the only layer in the model that is platform-specific. In essence, this layer is a wrapper for the standard socket APIs that can construct and send various packet formats.

Como o protocolo de comunicação utilizado é "não confiável", os desenvolvedores devem criar mecanismos para que certos tipos de dados sejam enviados/recebidos de forma confiável. Esta confiabilidade deve ser garantida em camadas acima como "ghost manager", "move manager", etc.

connection manager

The job of the connection manager is to abstract the connection between two computers over the network. It receives data from the layer above it, the stream manager, and transmits data to the layer below it, the platform packet module. The connection manager level is still unreliable. It does not guarantee delivery of data sent to it. However, the connection manager does guarantee a delivery status notification — that is to say, the status of a request passed to the connection manager can be verified. In this way, it is possible for the level above the connection manager (the stream manager) to know whether or not particular data was successfully delivered. The delivery status notification is implemented with a sliding window bit field of acknowledgments. 

stream manager

The primary job of the stream manager is to send data to the connection manager. One important aspect of this is determining the maximum rate of data transmission that is allowed. This will vary depending on the quality of the Internet connection.

An example given in the original paper is where a user on a 28.8-kbps modem might have their packet rate set to 10 packets per second with a maximum size of 200 bytes per packet, for approximately 2 kB of data per second. This rate and size is sent to the server upon connection of the client, in order to ensure that the server does not overwhelm the client’s connection with too much data.

Since several other systems will ask the stream manager to send data, it is also the duty of the stream manager to prioritize these requests. The move, event, and ghost managers are given the highest priority when in a bandwidth-bound scenario. Once the stream manager decides on what data to send, the packets are dispatched to the connection manager. In turn, the higher-level managers will be informed by the stream manager regarding the status of delivery.

Because of the set interval and packet size enforced by the stream manager, it is very much possible for a packet to be dispatched with multiple types of data in it. For example, a packet may have some data from the move manager, some data from the event manager, and some data from the ghost manager.

Event Manager

The event manager maintains a queue of events that are generated by the game’s simulation. These events can be thought of as a simple form of a remote procedure call or RPC, a function that can be executed on a remote machine. The server will validate and execute the game simulatiin event.

It is also the purview of the event manager to prioritize the events — it will try to write as many of the highest priority events as possible until any of the following conditions are true: the packet is full, the event queue is empty, or there are currently too many active events.

The event manager also tracks the transmission records for each event marked as reliable. In this way, it is very simple for the event manager to enforce reliability. If a reliable event is unacknowledged, then the event manager can simply prepend the event to the event queue and try again. Of course, there will be some events that are marked as unreliable. For these unreliable events, there is no need to even track their transmission records.

ghost manager

At a high level, the job of the ghost manager is to replicate or "ghost" dynamic objects that are deemed relevant to a particular client. In other words, the server sends information about dynamic objects to the clients, but only the objects that the server thinks the client needs to know about. The game's simulation layer is responsible for determining what a client absolutely needs to know and what a client ideally should know. This adds an inherent prioritization to game objects in the world: "need to know" objects are the highest priority, while "should know" objects are lower priority. In order to determine whether or not an object is relevant to a particular client, there are several different approaches that can be employed. In general, determining object relevancy is very game-specific.

Regardless of how the set of relevant objects is computed, the job of the ghost manager is to transmit object state from server to client for as many relevant objects as possible. It’s very important that the ghost manager guarantees that the most recent data is always successfully transmitted to all of the clients. The reason for this is that the game object information that is ghosted will often contain information such as health, weapons, ammo count, and so on—all cases where the most recent data is the only information that matters.

When an object becomes relevant (or “in scope”), the ghost manager will assign some information to the object, which is appropriately called a ghost record . This record will include items such as a unique ID, a state mask, the priority, and status change (whether or not the object has been marked as in or out of scope).

For transmission of the ghost records, the objects are prioritized first by status change and then by the priority level. Once the ghost manager determines the objects that should be sent, their data can be added to the outgoing packet using an approach similar to what is covered in  Chapter 5 , "Object Replication." 

move manager

The responsibility of the move manager is to transmit player movement data as quickly as possible. If the information regarding a player's position is slow to arrive, it could result in players shooting at where a player used to be instead of where a player is, which can result in frustrating gameplay. Quick movement updates can be an important way to reduce the perception of latency on the part of player. 

The other reason the move manager is assigned a high priority is because input data is captured at 30 FPS. This means there is new input information available 30 times per second, so the latest data is sent as quickly as possible. This higher priority also means that, when move data is available, the stream manager will always first add any pending move manager data to an outgoing packet. Each client is responsible for transmitting their move information to the server. The server then applies this move information in its simulation of the game, and acknowledges the receipt of the move information to the client who sent it. 


# Networking model in RTS

Example of networking model: _Age of Empires_ (1990)

_Age of Empires_ uses a **deterministic lockstep** networking model.

Neste modelo, cada computador se conecta diretamente com os outros diretamente - topologia de rede **peer-to-peer**. O termo "determinístico" significa que todos os computadores (peers) recebem as mesmas entradas, executam os mesmos passos e chegam no mesmo resultado. O termo "lockstep" significa que os computadores utilizam a comunicação para se manter sincronizados. Este tipo de modelo de rede é utilizado até hoje em jogos do genêro RTS.

Uma vantagem de utilizar o modelo peer-to-peer é que os dados chegam mais rapidamente ao destino em comparação com o modelo client/server.

Os jogos RTS em geral possui a capacidade de jogadores limitada (por exemplo, no máximo oito jogadores na mesma sessão de jogo) mas uma quantidade enorme de unidades que podem ser gerenciadas por cada jogador (por exemplo, cada jogador pode ter o controle de até 200 unidades).

A estratégia adotada neste modelo é sincronizar a lista de comandos executados pelos jogadores em vez de sincronizar as informações de cada unidade relevante. Isto significa que cada instância de jogo precisa executar todos os comandos de todos os jogadores de forma independente e todas as instâncias de jogo precisam estar sincronizadas.

Cada jogador pode executar o jogo com diferentes taxas de quadros e qualidade de conexão. Para que as instâncias de jogo fiquem sincronizadas, os comandos emitidos por cada jogador precisam ser enviados a todos os jogadores antes de serem executados. O mecanismo utilizado para gerenciar estes comandos e não perder a responsividade é chamado de **Turn Timer**.

Neste método, cada turno tem um tempo de duração ```length``` (por exemplo, 200ms). Todos os comandos emitidos dentro desta janela de tempo são armazenados em um buffer. Quando a duração acabar, os comandos armazenados no buffer são enviados para todos os outros jogadores. Outro aspecto de Turn Timer é o delay de execução de turnos (por exemplo, delay de dois turnos). Isso significa que os comandos gerados em um turno serão executados depois de dois turnos, provocando um input lag de 600ms neste exemplo.

Outro ponto a se considerar é quando um jogador sofre "lag spike" e ultrapassa o limite de tempo do Turn Timer para receber respostas da rede. Alguns jogos utilizam o "pause" para aguardar a melhora de conexão do jogador ou "expulsam" o jogador da partida após certo tempo de espera. O jogo poderia também dinamicamente ajustar a taxa de quadros do jogo baseado nas condições de rede para compensar este cenário - os jogadores teriam um tempo maior para receber os dados da rede.

Uma outra situação, além da comunicação, que pode tornar as instâncias de jogo fora de sincroniza é o uso de aleatoridade no jogo (pseudo random number generator ou PRNG). Como todas as instâncias devem executar os mesmos comandos, todas as instâncias precisam possuir a mesma semente de aleatoridade para produzir os mesmos resultados. Vale lembrar que PRNG com sementes iguais garantem apenas a mesma sequência de números. Se por algum motivo, uma instância se perder na sequência gerada pelo PRNG, o jogo ficara fora de sincronia.

Um benefício interessante que o modelo **deterministc lockstep** tras é a possibilidade de reutilizar a lista de comandos da partida para criar replay de partidas jogáveis. A lista de comandos também pode ser utilizada para treinar IA e criar adversários que simulam jogadores reais. Além disso, é possível evitar vários tipos de cheats como um jogador que consegue alterar valores de unidades dentro do seu jogo, mas isso é facilmente identificado porque nas outras instâncias conterá valor diferente. Um ponto negativo é o famoso "maphack" - como todas as instâncias possuem comandos de todos os jogadores, é possíve hackear o jogo para exibir informações de outros jogadores.

# References

- GLAZER, J. MADHAV, S. Multiplayer Game Programming: architecting networked games. Addison-Wesley, 2016.  

Bettner, Paul and Mark Terrano. “1500 Archers on a 28.8: Network Programming in Age of
Empires and Beyond.” Presented at the Game Developer’s Conference, San Francisco, CA, 2001.
Frohnmayer, Mark and Tim Gift. “The Tribes Engine Networking Model.” Presented at the Game
Developer’s Conference, San Francisco, CA, 2001.
Koster, Raph. “Online World Timeline.” Raph Koster’s Website . Last modified February 20, 2002.
http://www.raphkoster.com/gaming/mudtimeline.shtml .
Kushner, David. Masters of Doom: How Two Guys Created an Empire and Transformed Pop Culture .
New York: Random House, 2003.
Morningstar, Chip and F. Randall Farmer. “The Lessons of Lucasfilm’s Habitat.” In Cyberspace: First
Steps , edited by Michael Benedikt, 273-301. Cambridge: MIT Press, 1991.
Wasserman, Ken and Tim Stryker. “Multimachine Games.” Byte Magazine , December 1980, 24-40.
