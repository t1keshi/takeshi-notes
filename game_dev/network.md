Previous: [Game Development](game_dev.md)  

# Multiplayer Game Development

In a client-server model, players all connect to a central server, whereas in a peer-to-peer model, every player connects to every other player.

A peer-to-peer model requires O(n2) bandwidth. This means that the bandwidth grows at a quadratic rate based on the number of users. In this case, with n being as high as 128, using peer-to-peer would lead to very little bandwidth per player.

In client-server model, the bandwidth requirements of each player remain constant, while the server must handle only O(n) bandwidth. However, this meant that the server needed to be on a network that would allow for several incoming connections—the type of connection. 


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


# Networking model in RTS

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

# References

- GLAZER, J. MADHAV, S. Multiplayer Game Programming: architecting networked games. Addison-Wesley, 2016.  
