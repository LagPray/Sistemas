# Configurando redes COMPLETO no Linux 

[Criação do documento, ainda está em desenvolvimento]

## *Nomenclatura e definições*

### Tipos de redes:

Static : Static (ou estática) é o tipo de rede que tem um endereço fixo, sempre definido pelo usuário.

DHCP : DHCP (Dynamic Host Configuration Protocol) é o tipo de rede que tem endereços IP atribuídos automaticamente por um servidor DHCP, podendo ser renovados periodicamente (lease time), mas não necessariamente mudando a cada conexão.

### Definições dos componentes:

####    Temos 2 padrões de nomes de placa de rede: o pré-2015 (padrão clássico ou simples) e o pós-2015 (padrão moderno ou Predictable).

Dentro do padrão clássico teremos sempre os seguintes componentes:

**eth**: Interface de rede Ethernet (conexão cabeada). É o nome padrão de placas de rede no modelo clássico.
**wlan**: A placa wifi ligada.

Agora, no padrão moderno sempre seguiremos as seguintes definições:

**[Um prefixo]**

en = **e**ther**n**et (conexão via cabo)
wl = **wl**an (conexão via wifi)
ww = **ww**an (conexão mobile)

**[A localização física na placa-mãe]** (Os exemplos abaixo serão apresentados com conexão Ethernet)

en**o** = "o" significa _on-board_, ou seja, já vem soldado na placa-mãe.
en**p**2**s**0 = "p" significa PCI e o "s" slot. Nesse exemplo a placa de rede está no barramento PCI 2, no slot 0.
en**s** = Nesse caso o "s" significa Hotplug slot, aparecendo muito comumente em máquinas virtuais.

**_Para ambos os casos (padrão moderno e clássico) sempre haverá mais um componente: o número da interface, usado para distinguir interfaces do mesmo tipo quando há mais de uma. O número da interface sempre será declarado, mesmo que haja apenas uma. A declaração é simples, sendo apenas um número subsequente ao nome da interface de rede. O número da interface é atribuído automaticamente pelo sistema e pode começar em 0 ou 1, dependendo da distribuição e do contexto. Por exemplo, _eth0_, eno2 ou _ens3_._**

Além desses componentes, também temos:

**loopback**: É a forma do sistema se comunicar consigo mesmo no que diz respeito ao envio de pacotes de dados, enviando os dados para o "caminho de saída" da rede do computador, mas antes de chegar lá é interceptado e enviado de volta à entrada da rede, criando um loop de retorno de pacotes de dados.
    O endereço padrão do loopback é _127.0.0.1_ e não há necessidade de ser declarado nas configurações da rede, mas também é possível ter uma sub-interface lógica, num alcance de 127.255.255.255, que pode ser usada para isolar serviços e no uso de servidores BGP.
    Posteriormente será apresentado como declarar uma sub-interface loopback.
    
#### Endereço do arquivo que tem as configurações de rede: `/etc/network/interfaces`
#### Configuração estática padrão : 
```
auto nome_da_placa_de_rede
iface nome_da_placa_de_rede inet static
    address (endereço de IP desejado)
    netmask (máscara da rede)
    gateway (IP do roteador)
    dns-nameservers (endereços de servidores DNS)
```
#### Configuração DHCP padrão :
```
auto nome_da_placa_de_rede
iface nome_da_placa_de_rede inet dhcp
```
Adições futuras à documentação:
Adicionar futuramente nessa seção uma melhor explicação sobre o arquivo interfaces, explicando cada declaração, como _auto_ ou _iface_.
Adicionar os comandos de rede como ifup, ifdown, ip a e ip show.
Adicionar futuramente a explicação e apresentação direcionada para diferentes sistemas, como RHEL e yaml.
Explicar sobre o arquivo resolv.conf que define o endereço de resolução DNS.
Explicar o que é cada coisa, como netmask, DNS, IPv4, IPv6 e range, por exemplo.
Explicar os privilégios necessários para editar cada arquivo de configuração da rede.
Explicar o que é um servidor DHCP e também um servidor BGP.
