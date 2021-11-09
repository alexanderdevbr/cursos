Professor: Adilson
Material.: encurtador.com.br/fAVX7

Versatile Routing Platform (VRP) - Sistema Operacional dos equipamentos Huawei
- CE as configurações são "like commit" e precisa ser confirmada
- As séries S57 já são aplicadas no momento da execução do comando

Emulador utilizado no curso eNSP


Comandos:
<> user-view (Administração)
[] system-view (Construção de Configuração global)

Arquivo de configuração fica no arquivo 'currentconfig' que é armazenado na memória ram. Para salvar as configurações devem ser feitas para o arquivo 'savedconfig' para persistência.
display current-configuration (mostra as configurações atuais)
display saved-configuration (mostra as configurações persistentes)
display this (Mostra configuração do item atual)
undo term mon (Desabilita log)
save (salva a configuração em memória para persistente)

quit - Volta um nível de configuração
return (ctrl + z) - Volta direto para user-view

Niveis de acesso [0 - 15], sendo 0 o menos privilegiado e o 15 o mais privilegiado

disp cur | b ospf (Begin)
disp cur | i int  (Include)
disp cur | e int  (Exclude)

Protocolo Spanning Tree Protocol - STP/RSTP/NSTP
------------------------------------------------
Ethernet <> IP
Ñ TTL       TTL

- Escolha de um SW raiz
    - Menor Prioridade (default 32768 / 800 hexa)
    - Menor MAC
- Caminhos secundários são bloqueados

Root Port por vLan permite fazer o balanceamento de carga entre as interfaces


Link Agregation - LAG
- 1 Porta lógica com várias interfaces físicas
- Maneira de "fugir do STP" e utilizar diversas portas
- Ideal trabalhar com qtde pares de interfaces físicas para melhor balanceamento e distribuição
- Protocolo de Link Agregation - LACP
    - Limite de 8 interfaces automático
    - Permite uso de interface de backup

Virtual Lan - VLAN
- Agrupamento Lógico de equipamentos
- Domínio de broadcast
- Rede lógica
- Segregar tráfego
- Segurança
- Vlan nativa normalmente usada para tráfego não tagueado
- Recomendação de mudança de vlan nativa para uma outra vlan (666)

Tipos de portas
- Acesso (geralmente com Vlans Tagueadas com dispositivos finais conectados. Porta de acesso pertence a somente uma determinada Vlan)
- Tronco (entre switchs, envia quadros não tagueados)
- Hibrida (Trabalha como Acesso e Tronco)


Tabela salva vidas IP
=============================
                256 - Octeto
Bits    Octeto  Variação
------- ------- --------
1       128     128
2       192     64
3       224     32
4       240     16
5       248     8
6       252     4
7       254     2
8       255     1

Exemplo:
172.16.0.0/21
255.255.248.0
SubRede..: 172.16.0.0
Broadcast: 172.16.7.255
Intervalo válido IPs: 172.16.0.1 até 172.16.7.254

www.subnetingquestions.com


Calculo de subredes
Subrede /12 cabe quantas subredes /16 ?
    16 - 12 = 4
    2 ^ 4 = 16 subredes dentro do /12

Qual máscara atende uma rede com 4000 hosts?
2 ^ 12 = 4096
Para atender 4000 hosts precisa de 12 bits "desligados",
32 bits - 12 bits = 20 bits "ligados", logo uma subrede /20 atende.



OSPF
- Tabela de Rotas dinâmicas
- Protocolo para descobrir qual melhor caminho
- Uso apenas para IPs privados
- Bom até umas 50k rotas
- Foi feito para grande redes de campos e possui uma estrutura hierarquica
    - Area 0 (Core de rede)
    - Area 1 .. N com pelo menos um roteador ligando com "Área 0"
    - Tudo passa pela "Area 0"
- Usa máscara "Invertida"
    - Mask      255. 255. 255.   0
      Mask OSPF   0.   0.   0. 255
- Tabela de roteamento quanto menor melhor


IPV6
- Data de 1998
- 128 bits (32 simblos HEX, 8 blocos de 4 simbolos')
- Zeros a esquerda podem ser cortados
- Blocos vázios com zeros podem ser suprimidos (uma única vez)
- Por usar HEX não faz diferença entre maiusculo e minusculo
- No maximo 64 bits para identificador rede


BGP / MPLS