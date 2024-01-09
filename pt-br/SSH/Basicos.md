# Vou explicar um pouco sobre o minimo que você precisa para usar o SSH!

## Executar comandos
Você pode executar comando de duas principais formas no SSH:

- Conectando-se ao sistema:
```bash
ssh vitor@21.21.21.21

whoami
vitor
```
- Executando de uma só vez:
```bash
ssh vitor@21.21.21.21 whoami
vitor
```
## Copiar arquivos com o SCP

- Mandar um arquivo da minha máquina para o sistema remoto.
```bash
scp molécula.xyz vitor@21.21.21.21:~/home/vitor
 ```

- Baixar um arquivo do sistema remoto
```bash
scp vitor@21.21.21.21:~/home/vitor/molécula.xyz ./moléculas/Cr2Si12
```

- Baixar uma pasta inteira do sistema remoto
```bash
scp -r vitor@21.21.21.21:~/home/vitor/molécula.xyz ./moléculas/
```

## Copiar arquivos com o SFTP

- Mandar um arquivo da minha máquina para o sistema remoto.
```bash
sftp vitor@21.21.21.21
sftp> put /loot/molécula.xyz /home/vitor/molécula.xyz
 ```

- Baixar um arquivo do sistema remoto
```bash
sftp vitor@21.21.21.21
sftp> get /home/vitor/molécula.xyz /loot/molécula.xyz
```
