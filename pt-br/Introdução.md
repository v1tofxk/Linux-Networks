# Construindo uma Rede Profissional 🌐

Nesse repositório, vou te instruir sobre como construir uma rede profissional aplicável! Além disso, darei algumas dicas de ataque e defesa na segurança da sua rede.

Vamos começar!
-----------

Bom, digamos que você tem dois computadores e deseja fazer uma comunicação entre eles. Para isso, cada um necessita de um "endereço" que seja único e eles possam enviar mensagens de um para o outro! Chamaremos esse endereço de **MAC address**.

Tecnicamente, o endereço MAC é uma sequência alfanumérica única representada por seis pares de números e letras, separados por dois pontos (por exemplo, `00:1A:2B:3C:4D:5E`). Cada fabricante de dispositivos de rede é atribuído um conjunto único de identificadores, conhecido como **OUI (Organizationally Unique Identifier)**, que faz parte do endereço MAC. Isso significa que os primeiros três pares do endereço MAC identificam o fabricante específico do dispositivo.

Para fazer a "ponte" entre esses dois dispositivos, é necessário um **switch**. Funcionará da seguinte forma: "Ei switch, esse é o meu MAC address e esse é o MAC address do destinatário, se vira aí!" O switch compara com a tabela e determina a porta do destinatário.

(!) **Nota**: Um broadcast storm pode ocorrer em redes com switches interconectados por dois cabos diferentes quando ocorre um loop na topologia da rede. É importante configurar switches com um protocolo de prevenção de loops, como o **Spanning Tree Protocol (STP)**.

------

Mas os MAC address têm um problema. Quando você decide trocar um equipamento, será necessário configurar tudo novamente com o endereço novo. Para resolver isso, temos endereços IP.

**IPv4** (exemplo: `192.168.1.1`):
- Composto por 32 bits, divididos em quatro octetos.
- Cada octeto é representado por um número decimal de 0 a 255.
- Enfrenta escassez de endereços devido à crescente quantidade de dispositivos conectados à internet.

**IPv6** (exemplo: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`):
- Composto por 128 bits, expressos em notação hexadecimal.
- Desenvolvido para superar a escassez de endereços do IPv4, fornecendo uma quantidade virtualmente ilimitada de endereços IP.

Assim como o endereço MAC, se o endereço IP for estático, toda vez que uma máquina nova entrar no jogo, você terá que mexer em toda a configuração. Para isso, temos o protocolo **DHCP**, que atribui endereços dinamicamente para cada dispositivo.

----------------------

Na maioria das vezes, você se conectará a algum hostname, e seu computador perguntará ao servidor DNS: "Ei, quem tem esse nome de host?". O DNS funciona como um sistema de tradução de nomes para endereços. Quando você digita um nome de domínio no seu navegador, o servidor DNS localiza o endereço IP associado ao nome de domínio.

**DNS**:
- Funciona como um sistema de tradução de nomes para endereços.
- Quando você digita um nome de domínio, o computador envia uma solicitação para um servidor DNS.

**ARP** (Address Resolution Protocol):
- ARP funciona como uma "lista telefônica" local da rede.
- Se um computador conhece o endereço IP de outro, mas não sabe o endereço MAC correspondente, ele envia um pedido ARP para descobrir.

**ARP**:
1. Solicitação ARP (ARP Request):
   - Um dispositivo na rede emite uma Solicitação ARP para descobrir o endereço MAC associado a um determinado endereço IP.
   - A solicitação é enviada para todos os dispositivos na rede local.

2. Resposta ARP (ARP Reply):
   - O dispositivo com o endereço IP correspondente responde com sua própria informação ARP.
   - A resposta ARP contém o endereço MAC associado ao endereço IP procurado.

3. Atualização das Tabelas ARP:
   - O dispositivo solicitante atualiza sua tabela ARP local com o par de endereços IP e MAC recém-descoberto.

4. Cache ARP:
   - Para evitar a repetição constante do processo, muitos dispositivos mantêm uma "cache ARP".

---------

## Mas e se você quiser se comunicar com "google.com", por exemplo? Temos servidores de encaminhamento e roteadores!

- Um servidor de encaminhamento permite que você não precise ter todos os domínios de rede localmente na sua rede.

- Os **roteadores** são essenciais. Quando o DHCP client enviar o endereço IP do seu dispositivo, ele também enviará um padrão gateway. Seu computador olhará para o endereço do Google e enviará o pacote para o roteador.

- Seu computador vai olhar para o endereço do google, e vai dizer "Nossa esse endereço é mt diferente do meu... então não vou fazer o que eu faria nas outras vezes, vou apenas pegar meu gateway padrão, obter seu endereço MAC e enviar esse pacote pro roteador e ele que se vire!!"

- Tentei resumir da forma mais simples para que você siga essa jornada sem muitas dúvidas, espero que tenha gostado do conteúdo!

