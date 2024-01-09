# O que é DHCP? 🔗

O **DHCP** (Dynamic Host Configuration Protocol) é um protocolo de rede usado para atribuir automaticamente configurações de rede a dispositivos em uma rede, como endereços IP, máscaras de sub-rede, gateways padrão e servidores DNS.

O serviço DHCP proporciona três benefícios para a organização:

1. **Redução de tarefas operacionais:** O administrador de rede não precisa mais configurar manualmente cada cliente antes que eles possam usar a rede.
2. **Otimização do plano de endereçamento IP:** Os endereços não utilizados são liberados e disponibilizados para novos clientes que se conectam.
3. **Gestão fácil da mobilidade do usuário:** O administrador não precisa reconfigurar manualmente um cliente quando seu ponto de acesso à rede é alterado.

---

Antes de prosseguir, certifique-se de que já realizou a prática de [gateway](https://github.com/v1tofxk/Linux-Networks/blob/main/pt-br/2.%20Gateways/Como%20configurar%20um%20gateway%20no%20linux.md).

Agora, instale o servidor DHCP:

```bash
sudo apt update
sudo apt install isc-dhcp-server -y
```
Irá aparecer uma mensagem de erro, mas isso é natural, pois o DHCP ainda não foi configurado.

O primeiro arquivo a ser configurado é o dhcpd.conf. Neste arquivo, será definido o plano de endereçamento da rede interna, bem como os parâmetros que permitem a customização do serviço para a organização.

```bash
sudo nano /etc/dhcp/dhcpd.conf
```

Para tornar o servidor DHCP oficial dos clientes, remova o comentário da linha 22 "authoritative;". Em seguida, vá para a seção "#this is a very basic subnet declaration." e adicione as seguintes informações:

```bash
subnet 192.168.200.0 netmask 255.255.255.0 {
 range 192.168.200.10 192.168.200.254;
 option routers 192.168.200.1;
 option domain-name-servers 8.8.8.8;
}

```
Agora, edite o arquivo /etc/default/isc-dhcp-server com as seguintes informações:`

```bash
DHCPv4_CONF=/etc/dhcp/dhcpd.conf
INTERFACESv4="enp0s8"
INTERFAVESV6=""
```
Inicie o serviço com o seguinte comando:

```bash 
sudo systemctl start isc-dhcp-server.service
```

E para confirmar, execute:
```bash
sudo systemctl status isc-dhcp-server.service

```

