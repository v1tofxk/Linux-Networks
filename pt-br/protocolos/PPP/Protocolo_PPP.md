# Protocolo PPP 🤝

## Breve Resumo

O **Protocolo PPP** é extremamente versátil e importante para a comunicação ponto a ponto, especialmente em ambientes de conexão temporária (como discagem), oferecendo recursos de negociação, autenticação e suporte a vários protocolos de rede.

## O que é?

É um protocolo de comunicação utilizado para estabelecer uma conexão direta entre dois dispositivos, como por exemplo um computador e um servidor de acesso à internet.

## Características

### Estabelecimento de Conexão

O PPP é projetado para estabelecer uma conexão ponto a ponto entre dois dispositivos. Ele fornece uma maneira de encapsular pacotes de dados para transmissão sobre a linha de comunicação. Resumindo, o PPP prepara os dados para transmissão adicionando informações necessárias, como cabeçalhos e trailers, para criar quadros PPP. Esses quadros são, então, transmitidos pela linha de comunicação escolhida. Essa encapsulação é essencial para garantir que os dispositivos conectados possam entender e interpretar os dados corretamente durante a comunicação.

### Negociação de Parâmetros

Antes de estabelecer a conexão, o dispositivo PPP pode negociar parâmetros de configuração, como métodos de autenticação, endereços de IP e opções de compressão de dados.

### Camada de Enlace

O PPP opera na camada física de enlace do modelo OSI.

### Suporte à Autenticação

O PPP suporta diversos métodos de autenticação, como o PAP e o CHAP.
- **PAP (Password Authentication Protocol):** O cliente envia seu nome de usuário e senha ao servidor. O servidor verifica essas informações e concede ou nega o acesso. (O PAP envia credenciais de texto simples, o que torna menos seguro.)
- **CHAP (Challenge Handshake Authentication Protocol):** Funciona usando um desafio e resposta durante o processo de autenticação. Quando a conexão é iniciada, o servidor desafia o cliente a provar sua identidade. O cliente responde ao desafio usando uma função criptográfica (hash) aplicada à senha e a outras informações. Se os resultados coincidirem, a autenticação é bem-sucedida.

### Suporte a Múltiplos Protocolos de Rede

O PPP pode encapsular pacotes de diferentes protocolos, como IP, IPX e IPv6.
- **IP (Internet Protocol):** IPv4 utiliza endereços de 32 bits, o que permite aproximadamente 4,3 bilhões de endereços únicos. Devido ao crescimento da internet, os endereços IPv4 estão se esgotando, levando ao desenvolvimento do IPv6.
- **IPX (Internetwork Packet Exchange):** Utiliza endereços de 32 bits, similar aos endereços IPv4. Com a diminuição do uso de redes NetWare, o IPX tornou-se menos comum e foi substituído por protocolos IP, especialmente em ambientes mais modernos.
- **IPv6 (Internet Protocol version 6):** Utiliza endereços de 128 bits, proporcionando uma quantidade vastamente maior de endereços (aproximadamente 3.4 x 10^38 endereços únicos).

### Negociação de Endereços IP

O PPP pode ser usado para atribuir dinamicamente endereços de IP aos dispositivos conectados, usando o protocolo IPCP para essa finalidade.
- **IPCP (Internet Protocol Control Protocol):** O IPCP é um protocolo de controle que faz parte do processo de negociação e configuração de parâmetros específicos do protocolo IP em uma conexão PPP.

### Detecção de Erros e Recuperação

O PPP inclui mecanismos para detectar erros de transmissão e realizar recuperação de dados se necessário, melhorando a confiabilidade da comunicação.
