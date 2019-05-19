# LABORATÓRIO REDES VIRTUAIS
<p align="justify">Em Redes de Computadores conforme aumenta sua complexidade, demanda de usuários e quantidade de equipamentos interconetados, problemáticas incipientes tornam-se um fator de preocupação, transformando a rede em um ambiente desforável a produtividade necessária do usuário.</p>

<p align="justify">O aumento escalar de uma rede impacta diretamente no aumento de colisão, envio de <i>broadcast</i>, bem como uma insegurança no ambiente, considerando que todos os departamento de uma empresa ou órgão encontram-se inteconectados na mesma redes. Para sanar estes problemas Virtual Lan (VLAN) são criadas, nos quais implementam-se no switch uma segmentação lógica na rede, mapeando as portas dos dispositivos dentro do segmento ao qual necessita-se fazer seu agrupamento, como por setor de uma empresa: Recurso Humanos, Contabilidade, Adminstrativo, etc. A Figura 01 apresenta um exemplo de rede com vlan no qual equipamentos em switchs distintos fazem parte da mesma vlan.</p>

<p align="center"><img src="images/vlan.jpg"  width="600" height="314" align="middle"/></p>
<h4 align="middle">Figura 01 - Virtual Lan (VLAN)</h4>

<p align="justify">Para que você possa configurar um ambiente totalmente funcional com controlador de domínio samba, ferramenta de administração do Samba RSAT e um cliente para o teste, criei um Appliance no link abaixo:</p>

[Appliance GNS3](https://drive.google.com/open?id=1k_6UyI9RjKqrBUSAVVpLnftYZu6_9aI7) 




<p align="justify">Conforme apresentado no diagrama de rede acima Fig. 01 o IP da interface <b>enp0s3</b> é 192.168.5.1, a senha tanto do usuário <b>root</b> como do usuário <b>aluno</b> é <b>123456</b></p>

<p align="justify">É importante pontuar que a memória reservada para as máquinas virtuais foram de 1255 MB, todavia podendo diminuir este tamanho, conforme configuração da máquina que estará executando o Appliance. Podemos observar a alocação de memória desejada na Fig. 02.</p>

<p align="center"><img src="images/samba/02_virtualbox.png"  width="800" height="493" align="middle"/></p>
<h4 align="middle">Figura 02 - Alocação de Memória VM</h4>


## INSTALAÇÃO SAMBA

<p align="justify">Para instalação do Samba devemos baixar os pacotes: samba, kerbero, smbcliente e winbind, conforme comando a seguir:</p>





<h3 align="left">5.1 - Entendo a Arquitetura de um Roteador</h3>

<p align="justify">Um roteador é um compador com função específica de interconectar redes, seu hardware funciona de uma maneira um pouco difererente de um computador pessoal, um dos principais fabricantes do mercado é a CISCO, no qual nosso laboratório estará orientado, a Figura 03, apresenta a arquitetura dos componentes principais de um roteador. </p>
<p align="center"><img src="images/03-roteador.png"  width="400" height="240" align="middle"/></p>
<h4 align="middle">Figura 03 - Componentes Roteador</h4>

*  <b>RAM</b> – Armazena as tabelas de roteamento e o arquivo de configuração temporário do roteador;<p>
* <b>NVRAM</b> – Armazena o arquivo de configuração que será utilizado na inicialização (startup config), não ocorre perca das informações armazenadas na NVRAM ao desligar o roteador;<p>
* <b>FLASH</b> - Armazena a imagem de inicialização do Sistema Operacional, possui a possibilidade armazenar várias imagens, retém seu conteúdo quando o roteador é desligado;<p>
* <b>ROM</b> -  Mantém instruções que definem o autoteste realizado na inicialização do roteador;<p>
* <b>Console</b> -  É uma interface de acesso direto ao roteador para sua manutenção e atualização de firmware em caso de percado de acesso externo;<p>
* <b>Interfaces</b> -  Conectam o roteador à rede para entrada e saída de pacotes, podem estar diretamenta conectadas na placa-mãe ou adicinadas através de módulos, em computadores pessoas são chamadas de placas de rede;<p>

<p align="center" ><img src="images/aviso-importante.png"  width="300" height="130" align="middle"/></p>
<p align="justify">Todas as configurações realizadas em um roteador são salvas na RAM, portanto é um dado volátil, ocorrendo o desligamento inesperado a configuração feita é <b>PERDIDA</b>, daí a necessidade de salvar constante o que foi realizado na NVRAM através do comando: <i>copy running-config startup-config</i>.</p>

<h3 align="left">5.2 - Preparando o Ambiente para Realizar o Laboratório</h3>

<p align="justify">Iremos utilizar um software de simualação de rede desenvolvido e disponibilizado pela própria CISCO, chamado Packet Tracer, ele pode ser executado até mesmo em computadores antigos de 32 bits, para fazer o download cadastre-se no curso:</p>


[Introduction to Packet Tracer](https://www.microsoft.com/pt-BR/download/details.aspx?id=45520)

<p align="justify">É um curso gratuíto de 10 horas, que não tem obrigatoriedade de sua realização, mas já disponibiliza conteúdo e a o download da ferramenta. O mais importante é que você pode até achar o arquivo de instalação do Packet Tracer na internert, todavia para liberar todas as funcionalidades da ferramenta é necessário um login criado no cadastro deste curso, vou disponiblizar a seguir o arquivo para download direto que salvei no google drive:</p>

[Packet Tracer - 32 bits](https://drive.google.com/open?id=10PJHweyAjtvTW5J4JWVAGVdsNSeJKk9f)

[Packet Tracer - 64 bits](https://drive.google.com/open?id=1v3oJeTjKZX5XFH3iwGnDYITVQ1u1FQG_)

[Packet Tracer - Linux](https://drive.google.com/open?id=10dGsuiEm2PqPYw1F5qqx2Pkdquy4sOBQ)

<p align="justify">Após o download faça a instalação do aplicativo que é muito simples, realize o login no mesmo, é o usuário que você cadastrou para ter acesso ao curso, e faça o download do arquivo do laboratório disponiblizado abaixo:</p>

[Laboratório - Roteamento Dinâmico RIP](https://drive.google.com/open?id=1H6cVuwK_GAYC0BXm2RTWAelJVvFJ1O6D)

Menu Options => Preferences
 
<h3 align="left">5.3 - Execução do Laboratório</h3>
<p align="justify">Ao abrir o arquivo baixado no link acima, o Packet Tracer será aberto com duas telas, uma com o wizard que apresentará seus acerto no final e a outra com o diagrama de rede no qual você irá configurar, Figura4. </p>
<p align="center"><img src="images/roteamento/04-lab-packettracer.png"  width="900" height="448" align="middle"/></p>
<h4 align="middle">Figura 04 - Laboratório Packet Tracer</h4>

<p align="justify">Objetivo do Laboratório:</p>
*  Congigurar o endereçamento IP em todos os dispositivos do ambiente;<p>
* Configurar o Roteamento Dinâmico RIP no <b>Router1</b> e <b>Router2</b> para que o <b>PC0</b> possa se comunicar com o <b>PC1</b>;<p>

