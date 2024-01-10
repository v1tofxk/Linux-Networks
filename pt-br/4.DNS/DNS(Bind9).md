# Configuração de Servidores DNS Privados com BIND9 🛸

## Introdução

Um DNS privado oferece maior controle, segurança e desempenho em comparação com o uso de servidores DNS públicos. Esses benefícios são especialmente relevantes para empresas que precisam garantir a integridade, confidencialidade e disponibilidade de seus serviços online.

---

## Configuração do Ambiente

### Máquinas Envolvidas

- **ns1**
  - Função: Servidor DNS Primário (master)
  - Nome: ns1.DarkUniversity.com.br
  - IP: 192.168.200.10

- **ns2**
  - Função: Servidor DNS Secundário (slave)
  - Nome: ns2.DarkUniversity.com.br
  - IP: 192.168.200.11

- **host1**
  - Função: Host para Teste
  - Nome: host1.DarkUniversity.com.br
  - IP: 192.168.200.2

- **gateway**
  - Função: Gateway da Rede
  - Nome: gateway.DarkUniversity.com.br
  - IP: 192.168.200.1

### Configuração do Nome das Máquinas

```bash
sudo nano /etc/hostname
sudo nano /etc/hosts
```
Coloque os nomes das máquinas (ns1, ns2, gateway e host1) e reinicie.

## Instalação dos Recursos em ns1 e ns2
```bash
sudo apt update -y
sudo apt install bind9 bind9utils bind9-doc -y
```
##Configuração do BIND no Modo IPv4 em ns1 e ns2
```bash
sudo nano /etc/default/bind9
```
Deixe assim:

```bash
RESOLVCONF=no
OPTIONS="-u bind -4"
```
Reinicie o BIND para aplicar as mudanças:
```bash
sudo systemctl restart bind9.service
```

# Configuração do Servidor DNS Primário (ns1)

## Configuração do named.conf.options
```bash
sudo nano /etc/bind/named.conf.options
```
Adicione uma lista trusted e parâmetros necessários:
```bash
acl "trusted" {
    192.168.200.10;
    192.168.200.11;
    192.168.200.2;
    192.168.200.1;
};

options {
    directory "/var/cache/bind";
    recursion yes;
    allow-recursion { trusted;};
    listen-on { 192.168.200.10; };
    allow-transfer { none; };
    forwarders {
        8.8.8.8;
        8.8.4.4;
    };

```
## Configuração do Arquivo Local
```bash
sudo nano /etc/bind/named.conf.local

```
Adicione as zonas:
```bash
zone "DarkUniversity.com.br" {
    type master
    file "/etc/bind/zones/db.DarkUniversity.com.br";
    allow-transfer { 192.168.200.11 ;};
};

zone "200.168.192.in-addr.arpa" {
    type master;
    file " /etc/bind/zones/db.192.168.200";
    allow-transfer { 192.168.200.11; };
};

```
# Criação dos Arquivos de Zona
## Arquivo de Zona de Encaminhamento (db.DarkUniversity.com.br)
```bash
sudo mkdir /etc/bind/zones
cp /etc/bind/db.local /etc/bind/zones/db.DarkUniversity.com.br
sudo nano /etc/bind/zones/db.DarkUniversity.com.br

```
Conteúdo:
```bash
# BIND data file for local 192 interface
$TTL    604800
@   IN  SOA ns1.DarkUniversity.com.br. admin.DarkUniversity.com.br. (
                3       ; Serial
                604800  ; Refresh
                86400   ; Retry
                2419200 ; Expire
                604800 )    ; Negative Cache TTL

; name servers - NS records
    IN  NS  ns1.DarkUniversity.com.br.
    IN  NS  ns2.DarkUnicersity.com.br.

; name servers - A records
ns1.DarkUniversity.com.br.    IN  A   192.168.200.10
ns2.DarkUniversity.com.br.    IN  A   192.168.200.11

; name servers - A records
host1.DarkUniversity.com.br.  IN  A   192.168.200.2
gateway.DarkUniversity.com.br.    IN  A   192.168.200.1

```
Arquivo de Zona Reversa (db.192.168.200)
```bash
sudo cp /etc/bind/db.127 /etc/bind/zones/db.192.168.200
sudo nano /etc/bind/zones/db.192.168.200

```
Conteúdo:
```bash
# BIND reverse data file for local loopback interface
$TTL    604800
@   IN  SOA DarkUniversity.com.br. admin.DarkUniversity.com.br. (
                3       ; Serial
                604800  ; Refresh
                86400   ; Retry
                2419200 ; Expire
                604800 )    ; Negative Cache TTL

; name servers
    IN  NS  ns1.DarkUniversity.com.br.
    IN  NS  ns2.DarkUniversity.com.br.

; PTR records
10  IN  PTR ns1.DarkUniversity.com.br. ; 192.168.200.10
11  IN  PTR ns2.DarkUniversity.com.br ; 192.168.200.11
1   IN  PTR gateway.DarkUniversity.com.br ; 192.168.200.1
2   IN  PTR host1.DarkUniversity.com.br ; 192.168.200.2

```
## Verificação e Teste
```bash
sudo named-checkconf
sudo named-checkzone DarkUniversity.com.br /etc/bind/zones/db.DarkUniversity.com.br
sudo named-checkzone 192.168.200.in-addr.arpa /etc/bind/zones/db.192.168.200
sudo systemctl restart bind9

```
# Configuração do Servidor DNS Secundário (ns2)
##  Configuração do named.conf.options
```bash
sudo nano /etc/bind/named.conf.options
```
Adicione a ACL e as opções:
```bash
acl "trusted" {
    192.168.200.10;
    192.168.200.11;
    192.168.200.1;
    192.168.200.2;
};

options {
    directory "/var/cache/bind";
    recursion yes;
    allow-recursion {trusted; };
    listen-on {192.168.200.11; };
    allow-transfer { none; };
    forwarders {
        8.8.8.8;
        8.8

```
