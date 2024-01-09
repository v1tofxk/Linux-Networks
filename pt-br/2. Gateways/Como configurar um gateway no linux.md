# Serviço de Internet Gateway 📡

Um roteador pode ser utilizado de duas formas:
- Como segmento de uma rede de uma organização que detém todos os meios de controle de todos os segmentos.
- Como uma ponte entre uma rede mais abrangente e uma menos abrangente (WAN e LAN).

## Exemplo de Segmentação
Uma organização possui diversos departamentos, como marketing e vendas. Cada departamento tem sua própria rede LAN. O roteador pode ser configurado para conectar essas redes locais e permitir a comunicação entre elas.

## Exemplo de Ponte
Uma empresa possui uma LAN interna para operações diárias e se conecta com uma filial remota ou a internet através da WAN. O roteador é usado como uma ponte entre a LAN interna e a WAN externa.

Nesse artigo, irei te ensinar como fazer um gateway do tipo ponte. Comece fazendo as configurações básicas que estão no fixado.

Após iniciar o comando `-ip addr-`, será possível observar que o Adaptador 1 da Virtual Machine Gateway é a `enp0s3` e o adaptador 2 é o `enp0s8`. Isso pode mudar de distribuição para distribuição.

---

Começaremos alterando o arquivo: `/etc/network/interfaces`

Então adicionaremos a seguinte configuração para o `enp0s8`:

```bash
auto enp0s8
iface enp0s8 inet static
	address 192.168.200.1
	netmask 255.255.255.0
	network 192.168.200.0
	broadcast 192.168.200.255
```
Reinicie.

Agora mude o DNS em /etc/resolv.conf:

```bash
nameserver 8.8.8.8
```
Agora vá para a máquina cliente, edite o arquivo /etc/network/interfaces.
Iremos alterar o enp0s3, então irá ficar assim:

```bash
auto enp0s3
iface enp0s3 inet static
	address 192.169.200.2
	netmask 255.255.255.0
	network 192.168.200.0
	gateway 192.168.200.1
	dns-nameservers 8.8.8.8

```
Reinicie a máquina e faça os seguintes testes com o comando ping:
```bash
ping -c 1 192.168.200.2 (no gateway)
ping -c 1 google.com (no gateway)
```
Agora no gateway, edite o arquivo: /etc/sysctl.conf
Descomente #net.ipv4.ip_foward=1
Agora iremos criar um binário para já inicializar o gateway com nossas configurações.
Criaremos um arquivo gateway.sh em /usr/local/sbin/, então naturalmente:
```bash
sudo nano /usr/local/sbin/gateway.sh
```

Utilizaremos o [iptables](https://youtu.be/Yee2INb9hlw?si=BAAgH-x4bPn6wOpx) então o script ficará assim:
```bash
#!/bin/bash
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
```
```bash
sudo chmod +x /usr/local/sbin/gateway.sh
sudo /usr/local/sbin/gateway.sh
```
Executando o script na inicialização do Linux:

```bash
sudo nano /etc/systemd/system/gateway.service
```
```bash
[Unit]
Description=Gateway
After=network.target

[Service]
ExecStart=/usr/local/sbin/gateway.sh

[Install]
WantedBy=multi-user.target

```
E para finalizar:

```bash
sudo systemctl enable gateway.service
```
