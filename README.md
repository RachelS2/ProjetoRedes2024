# ProjetoRedes2024
Projeto de aplicação da disciplina Redes de Computadores. Configuração de uma rede. Alunas: Elena, Patricia e Rachel.

# Relatório
## Trabalho de Redes 2024.1

### Descrição do Trabalho

Utilizando o CISCO PACKET TRACER você vai criar a rede lógica com as seguintes informações:
A empresa EPR (Empresa de Projetos de Rede), precisa criar a estrutura de sua rede de computadores, de maneira que atenda às seguintes necessidades.

#### Estrutura da Rede
- **Departamentos**: Engenharia, Compras, TI e Infraestrutura.
- **Cada departamento deve conter**:
  - 20 estações de trabalho
  - 2 servidores
  - 2 impressoras
  - Totalizando 24 hosts
- **Máscara de sub-rede**: /27 (Classe C), atendendo à necessidade de 24 hosts por sub-rede.
- **Topologia**: Estrela.
- **Numeração IPs**: Sequência nas sub-redes de acordo com a máscara adotada.
- **Switch Utilizado**: Cisco 2950-24 para cada departamento, interligando-os entre si.
- **VLANs**:
  - Configure uma VLAN em cada sub-rede.
  - Crie 2 VLANs por sub-rede: VLAN1 (portas 1-12) e VLAN2 (portas 13-24).
  - Cada VLAN contém 10 estações, 1 impressora e 1 servidor.

#### Configuração de IPs
- **Departamentos Engenharia e TI**: IPs estáticos.
- **Departamentos Compras e Infraestrutura**: IPs dinâmicos.

### Passos para a Implementação

#### 1. Criando as sub-redes dos setores da empresa
- **Hosts por sub-rede**: 20 computadores, 2 impressoras, 2 servidores, 1 switch (2950-24).
- **VLANs**: 2 VLANs por sub-rede (VLAN1: portas 1-12, VLAN2: portas 13-24).

#### 2. Cálculo de número de IPs e máscara de rede
- **Sub-redes necessárias**: 4.
- **Máscara de rede**: /27, permitindo 32 IPs endereçáveis (30 utilizáveis).
- **Rede de Classe C**: Endereços de 192.0.0.0 a 223.255.255.0.
- **IP escolhido**: 192.168.0.0/27.
- **Máscara de rede**: 255.255.255.224.

#### 3. Cálculo de sub-rede
- **Endereços IP por setor**:
  - Engenharia: 192.168.0.1 a 192.168.0.30 (Broadcast: 192.168.0.31)
  - Compras: 192.168.0.33 a 192.168.0.62 (Broadcast: 192.168.0.63)
  - TI: 192.168.0.65 a 192.168.0.94 (Broadcast: 192.168.0.95)
  - Infraestrutura: 192.168.0.97 a 192.168.0.126 (Broadcast: 192.168.0.127)

#### 4. Configuração de VLANs
- **IPs dinâmicos (DHCP)**: Configurados para Compras e Infraestrutura.
- **Sub-redes**:
  - Cada sub-rede tem 2 VLANs.
  - VLAN1 (servidor 1): 14 IPs.
  - VLAN2 (servidor 2): 14 IPs.

#### 5. Configuração do Switch
- **VLAN2**: Criada na VLAN Database.
- **Portas**:
  - VLAN1: Portas 1-12.
  - VLAN2: Portas 13-24.
