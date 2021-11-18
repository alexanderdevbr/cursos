Professor: Adilson
Material.: encurtador.com.br/fAVX7

Switch L2 - Somente MAC em uma mesma rede
Switch L3 - Possibilidade de roteamento entre redes distintas

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

Mostrando os IPs das interfaces
===============================
    display ip int brief
    *down: administratively down
    !down: FIB overload down
    ^down: standby
    (l): loopback
    (s): spoofing
    (d): Dampening Suppressed
    The number of interface that is UP in Physical is 2
    The number of interface that is DOWN in Physical is 9
    The number of interface that is UP in Protocol is 2
    The number of interface that is DOWN in Protocol is 9

    Interface                         IP Address/Mask      Physical   Protocol  
    Ethernet0/0/0                     unassigned           down       down      
    Ethernet0/0/1                     unassigned           down       down      
    GigabitEthernet0/0/0              unassigned           down       down      
    GigabitEthernet0/0/1              10.0.1.254/24        up         up        
    GigabitEthernet0/0/2              unassigned           down       down      
    GigabitEthernet0/0/3              unassigned           down       down      
    NULL0                             unassigned           up         up(s)     
    Serial0/0/0                       unassigned           down       down      
    Serial0/0/1                       unassigned           down       down      
    Serial0/0/2                       unassigned           down       down      
    Serial0/0/3                       unassigned           down       down   

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
==========
BGP
- Protocolo de roteamento trocado por um "sistema autônamo" AS (Entidade na internet independente que pode publicar e aprender)
    - 0 a 64511 são AS Públicos (EGP)
    - 64512 a 65535 são AS Privadas (IGP)
- Protocolo robusto que consegue transportar quantidade muito grande de rotas (usado naInternet e Grandes Datacenters)
- Lento (Faz helo a cada 60 segundos)
- Contrução de rotas é um 'trabalho artesanal'
- Frágil pois fica muito na mão do ser humano (Intervenção manual)
- AS-PATH atributo
    - é a qtde de saltos entre as AS
    - evita looping pois a publicação ocorre apenas uma vez
- Toda vizinhança BGP é uma comunicação TCP porta 179
- Aprende todas as rotas dos vizinhos
- Escolhe a melhor rota (Menor qtde de salto entre AS)
- Full-mesh (todo mundo conversa com todo mundo) - Fórmula: (N*(N-1))/2
Atributos BGP:
    - Entrada (No AS)
        - Prefered-Value, valor preferência quanto maior melhor (padrão 0), só serve no roteador local (um roteador), não funciona entre diferentes roteadores
        - Local-Preference, valor de preferência de roteador de saída (padrão 100), transita entre os roteadores e influencia todos os roteadores.
    - Saída
        - As-Path, artificialmente aumenta número de saltos (Prepend)
        - Med, quanto menor melhor e funciona quanto o roteador tem dois ou mais lins com uma mesma ISP. Esse atributo não se propaga para outras AS.


ACL
    - Somente uma ACL por direção (Outbound/Inbound) e por interface
    - Filtrp de pacotes (Firewall Básico)
    - Classificação (NAT, QoS, VPN, etc)
    - ACL Padrão define IP de origem (Posiciona mais próximo do destino)
    - ACL Extendida define IP/Porta/Protocolo (origem e destino) e pode posicionar próximo origem
    Funcionamento
        - Tudo que não for permitido é bloquado (Padrão)
        - Sequência de regras executado Top-Down
        - Quando uma regra é atendida as demais não são executadas
    - Identificação ACL no Mundo Hauwei
        - 2000 - 2999: Básica (Ip de Origem)
        - 3000 - 3999: Avançada (Ip de Origem, destino, protocolo, porta origem e destino)
        - 4000 - 4999: L2 (Endereço MAC)

Arquitetura AAA (Triple Way)
    - Autenticação (Quem é você)
    - Autorização  (O que você pode fazer)
    - Auditoria    (Tudo que fizer pode ser auditado)
    - Protocolos RADIOS (usuário comum) ou TACACS (usuário admin)

VRRP
    - Trabalha com VIP e VMAC virtual
    - Um dos roteadores é escolhido como Master
    - Maior prioridade é escolhido como Master
    - Preempitivo (Poder de volta), se a prioridade de algum dispositivo mudar uma nova eleição para Master pode ser feita
    - Prioridade default 100
    - Prioridade 255 quando o VIP é configurado na interface
    - Prioridade 0 faz desativar o dispositivo no VRRP

Analise de Qualidade da Rede - NQA
    - Teste em um dispositivo remoto
        - Atraso ICMP
        - Verifica conectividade
        - Etc.
    - Mede desemepnho da rede e colhe estatisticas
    - Resposta do resultado pode ser amarrada em "Track" para tomada de decisões

DHCP
    - Funcionamento "DORA"
        - DHCP Discovery
        - DHCP Offer
        - DHCP Request
        - DHCP Ack
    - Escopo configurado com uma faixa de endereços atribuída
    - Caso não consiga pegar um endereço, é atribuido um Ip 169.254.x.y (APIPA)
    - Problemas de "Starvation"/"Fake DHCP" (Feature DHCP Snooping)
    - DHCP Snooping
        - Recurso de segurança para Analisar mensagens DHCP
        - Controles para evitar que alguém suba um DHCP falso ou alguém consuma todo escopo DHCP (Faixa de IPs)