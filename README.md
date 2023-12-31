
# Projeto de Redes - Curso de DevOps - Vem Ser Tech Ada

## Equipe 1:

- hiago.deleon@gmail.com
- Juan Soto Sotelo
- Layse Roberta da Silva Araújo
- leonardovsestudos@gmail.com
- Renata Martins de Assis

## Objetivo

Criar duas redes diferentes e realizar a comunicação via ICMP entre uma e outra.

### Rede A

- 192.168.0.0/24
- 192.168.10.254 (Gateway)
- 192.168.10.253 (DHCP e DNS)

Criação de Outras 4 máquinas (4 pcs e um servidor) dentro da Rede Interna A utilizando DHCP para desktops, e IP fixo para Servidores.


### Rede B

- 172.15.0.254/24 
- 172.15.0.254 (Gateway) 
- 172.15.0.253 (DHCP e DNS)
- 172.15.0.252 (Servidor Web)

Criação de Outras 5 máquinas dentro da Rede Interna B (4 pcs e 2 servidores) utilizando DHCP para desktops, e IP fixo para Servidores.

## Equipamentos

- 1 Router 1841
- 2 Switches 2960 24TT
- 8 PCs
- 2 Servers - PT
- 1 módulo PT-HOST-NM-1CGE


O objetivo final, é que um dos Desktops da Rede A, consiga colocar em seu navegador interno, o endereço do Site do Servidor WEB que está na REDE B, e a página possa ser carregada corretamente, validando deste modo o Roteamento entre as Redes, DNS e a camada da Aplicação funcionando corretamente.

# Solução:
---------

![Solucao](/files/Projeto_Redes_solucao.png)

--->link da nossa [solucao](./Projeto_Redes_Equipe1.pkt)

## Configuração das Redes

Rede A:
-------
- Monte a rede com 4 PCs, um servidor e um switch na configuração estrela (switch na posição central).
- Conecte os dispositivos. 
- Configure o servidor DHCP com o IP estático:
    - 192.168.10.254 (Gateway)
    - 192.168.10.253 (DNS)

![Servidor DHCP](/files/server_DHCP.png)

- Configure  e ative o serviço DHCP:
    - 192.168.10.254 (Gateway)
    - 192.168.10.253 (DNS)

![Servico DHCP](/files/server_DHCP1.png)

- Para cada uma das PCs, configure o IP usando o protocolo DHCP. Dessa forma o servidor distribuira os IP's para cada computador.

![PCs IP](/files/pc1.png)



Rede B:
-------
- Monte a rede com 4 PCs, um servidor e um switch na configuração estrela (switch na posição central).
- Conecte os dispositivos.
- Configure o servidor DHCP com o IP estático:
    - 172.15.0.254 (Gateway) 
    - 172.15.0.253 (DNS)

![Servidor DHCP(1)](/files/server_DHCP(1).png)

- Configure  e ative o serviço DHCP:
    - 172.15.0.254 (Gateway) 
    - 172.15.0.253 (DNS)

![Servico DHCP(1)](/files/server_DHCP(1)1.png)

- Para cada uma das PCs, configure o IP usando o protocolo DHCP. Dessa forma o servidor distribuira os IP's para cada computador.

![PCs IP](/files/pc3(1).png)

- Servidor web:
    - Desligue o servidor e troque a placa de rede por uma PT-HOST-NM-1CGE (para melhorar o tráfego de navegação), ligue o servidor novamente.

![Servidor web](/files/server_web2ada.png)

    - Configure os IPs do servidor:
        - 172.15.0.254 (Gateway) 
        - 172.15.0.253 (DNS)
        
![Servidor web](/files/server_web2ada1.png)
        
    - Ative os serviços http
    
![Servidor web](/files/server_web2ada2.png)

## Configuração do Roteamento

- Ligue o roteador
- Incluia as redes A e B usando o protocolo de roteamento RIP.

![router](/files/router_ring.png)

- Verifique as conexões das redes A e B com o roteador e  configure as rotas das redes para as interfaces FastEthernet0/0 e FastEthernet0/1:

![router](/files/router.png)

![router](/files/router1.png)

## Configuração do DNS

Finalmente, nos servidores DHCP das redes A e B incluia os dns do servidor web da rede B

![DNSweb2](/files/server_DHCP2.png)


![DNSweb2](/files/server_DHCP(1)2.png)
  

## Testes

### Comunicação
---------------

- Abra um prompt de comando em um dos desktops da rede A e execute o comando ping para o endereço IP do servidor da rede B:

![comunicacao](/files/ping_pc0.png)


### Acesso WEB
---------------

- Teste o acesso HTTP ao servidor web da rede B usando o IP:
    - Abra um navegador da web em um dos PCs da rede A e insira o IP na barra de endereços.

![web_ip](/files/pc3webada.png)

- Teste o acesso HTTP ao servidor web da rede B usando o nome de domínio:
    - Abra um navegador da web em um dos PCs da rede A e insira o nome de domínio na barra de endereços.

![web_ip](/files/pc3webada1.png)
