
# Projeto de Redes - Curso de DevOps - Vem Ser Tech Ada

## Equipe 1:

- hiago.deleon@gmail.com
- Juan Soto Sotelo
- layseraraujo@gmail.com
- leonardovsestudos@gmail.com
- renataassis.17@gmail.com

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
    - Desligue o servidor e troque a placa de rede por uma PT-HOST-NM-1CGE, ligue o servidor novamente.

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

- Verifique as conexões das redes A e B com o roteador e  configure as rotas das redes para as interfaces Fa0/0 e Fa0/1:

![router](/files/router.png)

![router](/files/router1.png)



  

## Teste de Comunicação e DNS

Para testar a comunicação entre as redes e verificar o funcionamento do DNS, siga os passos abaixo:

1. Abra um prompt de comando em um dos desktops da rede 192.168.10.0/24.
2. Execute o comando `ping` para o endereço IP do servidor web na rede B:

```bash
ping 192.168.30.1
```

Se a comunicação for bem-sucedida, prossiga para o próximo passo.

3. Teste o DNS para verificar se é possível resolver nomes de domínio na rede B. Execute o comando:

```bash
nslookup redes
```

Esse comando tentará resolver o nome de domínio "redes" usando o servidor DNS configurado para a rede B (192.168.30.1). Se a resolução for feita com sucesso, você receberá uma resposta com o endereço IP correspondente ao nome de domínio.

4. Teste o acesso HTTP ao servidor web na rede B usando o nome de domínio. Abra um navegador da web em um dos desktops da rede A e insira o seguinte na barra de endereços:

```
http://redes
```

Isso tentará acessar o servidor web na rede B usando o nome de domínio configurado. Se a comunicação estiver funcionando corretamente e a resolução de DNS estiver configurada adequadamente, você verá a página web correspondente da Cisco.

## Conclusão

Com isso, concluímos a configuração das duas redes e a comunicação entre elas.

---
