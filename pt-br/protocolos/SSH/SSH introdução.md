# Introdução ao protocolo SSH! 💡
[(!) Referencia](https://www.youtube.com/watch?v=bh7DwPtYkrY&list=PLJE51qhGRWYUWXfgX1_SHe-Dqp1faIV7_)

## Pra que serve?
- O SSH veio para tornar seguro a forma de se acessar terminais, assim substituindo (não completamente) o Telnet.
- Além de acesso remoto, o SSH dá a oportunidade de "tunelamento" que permite os usos de protocolos não seguros

## Funcionalidades:
- Autentificação com chave pública: pode-se usar certificados para autentificação ao invés de digitação de senhas (Evita dor de cabeça)
- Redirecionamento de portas: qualquer sessão utilizando o protocolo TCP pode ser direcionado em uma sessão de SSH
- Redirecionando serviços X11: o SSH possibilita o redirecionamento de sessões X11
- Transferência de arquivos: o protocolo provê os serviços de SCP e SFTP para transferencia de arquivos

## Arquivos de configuração:
Em muitas distribuições linux o arquivo pode ser localizado em:

- cliente:
```bash
/etc/ssh/ssh_config
```

- Servidor:
```
/etc/ssh/sshd_config
```
