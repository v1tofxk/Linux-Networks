# Transformando sua Raspberry Pi em uma VLAN 🍒

## Introdução

A criação de uma Virtual LAN (VLAN) em uma Raspberry Pi pode ser uma solução valiosa para segmentar redes, melhorar a segurança e otimizar o desempenho. Este tutorial fornecerá instruções passo a passo sobre como configurar uma VLAN em sua Raspberry Pi, destacando os motivos para realizar essa transformação e abordando possíveis problemas.

## Motivos

Imagine que você queira que um dispositivo se comunique com várias VLANs, por exemplo um servidor que deveria estar disponivel para todos em cada VLAN.
Com um raspberry Pi você pode configurar varias portas e cada uma estará em uma VLAN diferente, também atribuindo um IP address pra cada uma!

## Pré-requisitos

Antes de começarmos, certifique-se de ter uma Raspberry Pi funcional, um sistema operacional Linux instalado e acesso à internet. a configuração é parecida com a da aula de [gateway](.)

## Vamos começar!

Na configuração de seu switch, coloque o Raspberry PI na VLAN 1, assim você poderá se conectar á ele com o protocolo [SSH](.)

```bash
sudo apt install vlan
```
```bash
sudo nano /etc/network/interfaces.d/vlan2
```
Agora iremos fazer a configuração da nossa vlan, repare que se você tiver varias outras VLANs você pode apenas alterar tudo que está "2", apenas colocando 3, 4 etc...

```bash
auto eth0.2
iface eth0.2 inet static
  vlan-raw-device eth0
  address 10.1.2.254/24
```
Salve tudo e de um restart na rede

```bash
sudo systemctl restart network
```
## Pronto agora seu Raspberry pi é um "Switch" com uma VLAN

Redes Domésticas ou Pequenas Empresas: Para usuários avançados que desejam maior controle sobre sua rede doméstica ou pequena empresa, um Raspberry Pi pode ser uma solução de baixo custo para implementar VLANs e segmentar dispositivos. 🍒
