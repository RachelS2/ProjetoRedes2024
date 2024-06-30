# ProjetoRedes2024
Projeto de aplicação da disciplina Redes de Computadores. Configuração de uma rede. Alunas: Elena, Patricia e Rachel.

```markdown
# Relatório
## Trabalho de Redes 2024.1

### Descrição do Trabalho
Utilizando o CISCO PACKET TRACER você vai criar a rede lógica com as seguintes informações:
A empresa EPR (Empresa de Projetos de Rede), precisa criar a estrutura de sua rede de computadores, de maneira que atenda às seguintes necessidades.

São 4 departamentos: Engenharia, Compras, TI e Infraestrutura.
- Cada departamento deve conter: 20 estações, 2 servidores e 2 impressoras, totalizando 24 hosts.
- Deve ser usada uma máscara de sub-rede que atenda a necessidade apresentada.
- A rede é de Classe C e deve-se usar a topologia estrela.
- Para a numeração IPs, deve-se usar uma sequência nas sub-redes de acordo com a máscara adotada.
- Como são 24 hosts em cada sub-rede, devemos usar uma máscara que permita esta configuração: neste caso a rede seria de /27, o host de 24.
- Descreva a rede, seu 1º IP válido, último IP válido e o broadcast de cada Sub-Rede.
- Utilize o switch 2950-24 da Cisco para cada departamento, interligando eles entre si.
- Cada departamento deve estar em uma sub-rede. Configure uma Vlan nas sub-redes. Configure uma VLAN nas sub-redes. Em cada Sub-rede crie 2 vlans com 12 portas
 cada. Da 1-12 VLAN1 e da 13 a 24 VLAN2. Cada VLAN vai ter 10 estações, 1 impressora e um servidor.
Os departamentos de Engenharia e T.I. Interno devem ser colocados IPs estáticos, já nos departamentos de compras e Infraestrutura devem ser colocados IPs
dinâmicos, de maneira que siga a sequência dos IPs estáticos.

### Criando as sub-redes dos setores da empresa
(commit ec009dd)
Utilizando as ferramentas do Cisco Packet Tracer, foram inseridos 20 computadores, 2 impressoras, 2 servidores (24 hosts) e 1 switch do tipo 2950-24 em cada
sub-rede, seguindo a descrição do enunciado.
Criação de duas redes virtuais (VLAN) dentro do switch, ou seja, o switch foi dividido, via software, de modo que um pedaço das portas atenda um grupo de 10
computadores, 1 impressora e 1 servidor e outro pedaço atenda outro grupo, que tem os mesmos hosts. Isso foi feito porque o objetivo do projeto é que esses dois
 grupos de cada sub-rede não se comuniquem.
Conforme a descrição do trabalho, a primeira VLAN corresponde as portas 1 à 12 e a segunda VLAN corresponde as portas 13 a 24.

### Cálculo de número de IPs e máscara de rede
Como são 4 setores no contexto do projeto, é preciso configurar 4 sub-redes, sendo que cada uma delas deve ter as seguintes características:

Como existem 24 hosts em cada departamento, é necessária uma máscara de rede /27, pois essa máscara gera 2^(32 - 27) = 2^5 = 32 IPs endereçáveis. Vale ressaltar
que uma máscara de rede define o intervalo de endereços IP que podem ser usados dentro de uma rede ou sub-rede.

Conforme descrito no trabalho, as sub-redes serão de Classe C, que é caracterizada por possuir um conjunto de endereços que vão de 192.0.0.0 até 223.255.255.0.

Os IPs serão restritos, pois trata-se de uma rede empresarial e as informações e a identidade on-line devem ser protegidas. Portanto, foi selecionado o padrão
192.168.0.0/27 (formato CIDR) desse tipo de IP, pois ele está na faixa de endereços da classe C.

O formato CIDR não é aceito pelo Cisco Packet Tracer, portanto, é necessário convertê-lo para a forma padrão. Para isso, basta construir uma sequência de 27 bits
um e 5 bits zero, totalizando 32 bits que um IP deve ter: 11111111.11111111.11111111.11100000.
Convertendo esse número para decimal, obtém-se a máscara de rede no formato desejado: 255.255.255.224

A rede é de topologia estrela é caracterizada por um elemento central que "gerencia" o fluxo de dados da rede, estando diretamente conectado a cada nó.

### Cálculo de sub-rede
Como descrito no tópico 3 deste relatório, para endereçar 24 hosts em cada setor, foi selecionada uma máscara de rede /27, pois ela permite até 32 endereços
(equivalente ao salto). Porém, o primeiro endereço é reservado para representar a sub-rede e o último é reservado para representar a difusão de mensagens na
sub-rede (broadcast). Por isso, 30 IPs podem ser utilizados pelos hosts de cada rede.
O salto no endereçamento de cada sub-rede é de 32 e o padrão de IP escolhido é o 192.168.0.0, sendo que os três primeiros octetos correspondem a parte de rede
do IP e o último octeto, em vermelho na tabela, representa a parte do host. Isso significa que o primeiro setor vai ter um endereço de rede cujo os hosts podem
assumir valores de 1 a 30 (pois o 0 é reservado a rede e o 31 é reservado ao broadcast), o segundo setor, valores de 33 à 62 (seguindo a mesma lógica) e assim
sucessivamente.

| Setores       | Rede          | Hosts                       | Broadcast       |
| ------------- | ------------- | --------------------------- | --------------- |
| Engenharia    | 192.168.0.0   | 192.168.0.1 até 192.168.0.30 | 192.168.0.31    |
| Compras       | 192.168.0.32  | 192.168.0.33 até 192.168.0.62| 192.168.0.63    |
| TI            | 192.168.0.64  | 192.168.0.65 até 192.168.0.94| 192.168.0.95    |
| Infraestrutura| 192.168.0.96  | 192.168.0.97 até 192.168.0.126| 192.168.0.127  |

### Configuração de VLANs
Os setores “Compras” e “Infraestrutura” têm IPs dinâmicos que foram alocados pelo DHCP. Em seguida, configuramos as VLANs de cada sub rede. Vale lembrar que uma
VLAN (Virtual Local Area Network) é uma forma de separação lógica entre LANs que traz melhorias na segurança, desempenho e administração da rede.
Cada subrede tinha duas VLANs. A primeira delas foi direcionada para o servidor 1, que atende 14 IPs e a segunda foi direcionada para o servidor 2, que também
atende 14 IPs. Dessa forma, cada servidor só podia se comunicar com um grupo de hosts.

### Configuração do Switch
No switch nós criamos uma VLAN2 na VLAN Database, depois separamos as portas 1-12 para a VLAN 1 e as portas 13-24 para a VLAN 2.
```
