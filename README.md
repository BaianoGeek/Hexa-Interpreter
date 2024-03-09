# Interpretador de Pacotes de Rede

Este é um script Python para interpretar pacotes de rede a partir de dados hexadecimais.

## Funcionalidades

- **Interpretação Ethernet**: Extrai informações do cabeçalho Ethernet, como MAC de destino, MAC de origem e tipo de protocolo.
- **Interpretação IP**: Extrai informações do cabeçalho IP, incluindo versão, tamanho do cabeçalho, tamanho total do pacote, TTL, protocolo, endereço IP de origem e endereço IP de destino.
- **Interpretação TCP**: Extrai informações do cabeçalho TCP, como portas de origem e destino, e flags TCP.
- **Extração de Payload**: Extrai o payload do pacote e o converte para texto ASCII.

## Uso

1 - No terminal, digite:
```
python3 hexaInterprer.py
```

2 - Insira os dados hexadecimais quando solicitado.

Exemplo de entrada:

d5 ac 83 46 c5 0d 01 0d 28 77 44 e2 08 00 46 01
82 08 01 41 01 41 07 01 06 9d e4 c1 a7 01 c9 26
3c af e9 dc 85 01 55 f0 4a 5c 3d 9a 97 0d be 81
1a 01 e4 98 08 01 01 09 0b 6c 42 27 5e 0a 67 38
95 48 46 55 21 2e 21 49 55 54 50 2f 32 2f 32


## Dependências

Este script Python não possui dependências externas.


## Exemplo de Saída:

====================ETHERNET====================

- Mac de Destino           d5:ac:83:46:c5:0d
- Mac de Origem            01:0d:28:77:44:e2
- Tipo de Protocolo        08 00

=======================IP=======================

- Versão                  IPv4
- Tamanho do Cabeçalho    24
- Tamanho tot. do pacote  33288
- TTL                     7
- Protocolo               01
- IP de Origem            228.193.167.1
- IP de Destino           201.38.60.175

=======================TCP======================

- Porta de Origem         59868
- Porta de Destino        34049
- Flags                   129 : FIN

====================Payload====================
