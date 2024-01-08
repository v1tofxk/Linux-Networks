# VLANs 🧰

Oi gente! Hoje vim explicar um pouco sobre VLANs e por que usá-las!

---

## Necessidade:

Geralmente, não desejamos que todos os computadores se conectem, principalmente porque, se apenas um dos computadores estiver infectado, pode acabar infectando todos os outros. Para resolver isso, as VLANs se tornam uma alternativa viável!

## Como Funciona:

As VLANs permitem que você "sub-divida" sua rede, criando "sub-redes" (se necessário). Assim, você pode realmente controlar a comunicação entre essas redes.

---

## Exemplo Prático:

Suponha que temos dois switches, Switch A e Switch B, com três computadores cada. Inicialmente, todos estão na mesma VLAN (VLAN 1).

```bash
Switch A                     Switch B
+---+---+---+               +---+---+---+
| 1 | 2 | 3 |               | 4 | 5 | 6 |
+---+---+---+               +---+---+---+
```

### Configuração Inicial:

- Todos os computadores (1, 2, 3, 4, 5, 6) pertencem à VLAN 1.
- Os Switches A e B estão configurados para a VLAN 1 por padrão.

### Criando VLANs:

- Configuramos o Switch A para ter duas VLANs (1 e 2).
- Configuramos o Switch B para ter as mesmas duas VLANs (1 e 2).

### Atribuindo Portas às VLANs:

- Atribuímos as portas 1, 2 e 3 do Switch A à VLAN 1.
- Atribuímos as portas 4, 5 e 6 do Switch B à VLAN 2.

### Bloqueando com Sucesso:

Se um computador em uma porta do Switch A tentar se comunicar com um computador em uma porta do Switch B, a comunicação será bloqueada porque eles estão em VLANs diferentes e não compartilham o mesmo domínio de broadcast.

---

## E Quando Eu Desejo Acrescentar Mais Um Switch?

Bom, digamos que você já tenha 1 switch e deseja adicionar mais 2.

- Configuração inicial:
```bash
Switch A
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
   |
   v
+---+
| PC|
+---+

```

Agora, adicionamos dois novos switches (Switch B e Switch C) à rede. Além disso, configuramos VLANs para isolar o tráfego. VLAN 1 ainda está presente, mas agora também temos VLAN 2.
```bash
Switch A (VLAN 1)          Switch B (VLAN 1)          Switch C (VLAN 2)
+---+---+---+             +---+---+---+             +---+---+---+
| 1 | 2 | 3 |             | 1 | 2 | 3 |             | 1 | 2 | 3 |
+---+---+---+             +---+---+---+             +---+---+---+
   |                          |                         |
   v                          |                         |
+---+                        |                         |
| PC|<-----------------------+                         |
+---+                                                   |
                                                        |
                                                        v
                                                     +---+
                                                     | PC|
                                                     +---+

```
- Agora, se um dispositivo em VLAN 1 (por exemplo, PC 1) quiser se comunicar com um dispositivo em VLAN 2 (por exemplo, PC no Switch C), a comunicação passará pelo roteamento. Pode ser necessário um roteador ou uma camada 3 switch para permitir essa comunicação inter-VLAN.
- Os switches mantêm a separação lógica entre as VLANs, bloqueando automaticamente o tráfego entre elas, a menos que haja uma rota configurada para permitir o tráfego.


## Configurações finais
Lembrando que geralmente, por questões de segurança, o tráfego entre VLANs não é permitido. A configuração difere entre os modelos de switch, então provavelmente você terá que ler o manual para saber como fazer o que você quer. (Nessas aulas, em muitos casos, trarei os conceitos e métodos, e poucas ferramentas, pois elas mudam com o tempo).
