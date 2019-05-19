# LABORATÓRIO REDES VIRTUAIS
<p align="justify">Em Redes de Computadores conforme aumenta sua complexidade, demanda de usuários e quantidade de equipamentos interconetados, problemáticas incipientes tornam-se um fator de preocupação, transformando a rede em um ambiente desforável a produtividade necessária do usuário.</p>

<p align="justify">O aumento escalar de uma rede impacta diretamente no aumento de colisão, envio de <i>broadcast</i>, bem como uma insegurança no ambiente, considerando que todos os departamento de uma empresa ou órgão encontram-se inteconectados na mesma redes. Para sanar estes problemas Virtual Lan (VLAN) são criadas, nos quais implementam-se no switch uma segmentação lógica na rede, mapeando as portas dos dispositivos dentro do segmento ao qual necessita-se fazer seu agrupamento, como por setor de uma empresa: Recurso Humanos, Contabilidade, Adminstrativo, etc. A Figura 01 apresenta um exemplo de rede com vlan no qual equipamentos em switchs distintos fazem parte da mesma vlan.</p>

<p align="center"><img src="images/vlan.jpg"  width="650" height="340" align="middle"/></p>
<h4 align="middle">Figura 01 - Virtual Lan (VLAN)</h4>

<p align="justify">No laboratório será criado um ambiente similar ao apresentado na Figura 01, para isso iremos utilizar o Software de Simulação de Rede para equipamentos da CISCO <a href="https://www.gns3.com/">GNS3</a>, vale ressaltar que o GNS3 possui suporte para executar de Container Docker, no qual será utilizado um Container com Debian. Preparei um Appliance que já vem com as imagens do IOS (Sistema Operacional CISCO), bem como o GNS3 instalado no link abaixo:</p>

[Appliance GNS3](https://drive.google.com/open?id=1F8LG6MlVq109AkOACGeWDzx50pdhm2w2) 


<p align="justify">O usuário padrão para login na interface gráfica do sistema é <b>gns3</b> e a senha tanto deste usuário quanto do <b>root</b> é  <b>123456</b></p>


<h3 align="left">1 - Entendo a Arquitetura dos Equipamentos da CISCO</h3>

<p align="justify">Um roteador e um switch é um compador com função específica de interconectar redes, seu hardware funciona de uma maneira um pouco difererente de um computador pessoal, no qual nosso laboratório estará orientado, a Figura 02, apresenta a arquitetura dos componentes principais de um roteador. </p>

<p align="center"><img src="images/03-roteador.png"  width="400" height="240" align="middle"/></p>
<h4 align="middle">Figura 02 - Componentes Roteador</h4>

*  <b>RAM</b> – Armazena as tabelas de roteamento e o arquivo de configuração temporário do roteador;<p>
* <b>NVRAM</b> – Armazena o arquivo de configuração que será utilizado na inicialização (startup config), não ocorre perca das informações armazenadas na NVRAM ao desligar o roteador;<p>
* <b>FLASH</b> - Armazena a imagem de inicialização do Sistema Operacional, possui a possibilidade armazenar várias imagens, retém seu conteúdo quando o roteador é desligado;<p>
* <b>ROM</b> -  Mantém instruções que definem o autoteste realizado na inicialização do roteador;<p>
* <b>Console</b> -  É uma interface de acesso direto ao roteador para sua manutenção e atualização de firmware em caso de percado de acesso externo;<p>
* <b>Interfaces</b> -  Conectam o roteador à rede para entrada e saída de pacotes, podem estar diretamenta conectadas na placa-mãe ou adicinadas através de módulos, em computadores pessoas são chamadas de placas de rede;<p>

<p align="center" ><img src="images/aviso-importante.png"  width="300" height="130" align="middle"/></p>
<p align="justify">Todas as configurações realizadas em um roteador são salvas na RAM, portanto é um dado volátil, ocorrendo o desligamento inesperado a configuração feita é <b>PERDIDA</b>, daí a necessidade de salvar constante o que foi realizado na NVRAM através do comando: <i>copy running-config startup-config</i>.</p>

<h3 align="left">2 - Preparando o Ambiente para Realizar o Laboratório</h3>

<p align="justify">O ambiente de simulação proposto contará com 3 (três) switchs, 03 (três) vlans, 06 (seis) Container Debian e um Router que irá fazer a comunicação entre as vlans, a Figura 03, apresenta a arquitetura deste ambiente com nome de vlans, enderaçamento de interfaces e portas a serem usadas, é importante pontuar que ao criar este ambiente no GNS3 deve-se seguir rigorosamenete as portas apresentadas na imagem.</p>

<p align="center"><img src="images/projeto-vlan.png"  width="910" height="520" align="middle"/></p>
<h4 align="middle">Figura 03 - Laboratório vlan</h4>


<p align="justify">Para melhor visualização habilite a visualização das portas dos equipamentos, conforme apresentado na Figura 04, Menu View => Show/Hide interface labes.</p>

<p align="center"><img src="images/interfaces-show.png"  width="400" height="441" align="middle"/></p>
<h4 align="middle">Figura 04 - Habilitar Visualização de Portas</h4>

<p align="justify">Os dispositivos de rede são adicinados pelo botão <b>Browse all devices</b>, apontado pela seta na Figura 5, clique e arraste os dispositivos para área de configuração, neste laboratório foram utilizados como Switch o <b>EtherSwitch c3727</b>, como Roteador o <b>Router C7200</b> e como cliente o <b>Container Debian</b></p>

<p align="center"><img src="images/devices.png"  width="400" height="513" align="middle"/></p>
<h4 align="middle">Figura 05 - Habilitar Visualização de Portas</h4>

<p align="center" ><img src="images/aviso-importante.png"  width="300" height="130" align="middle"/></p>

<p align="center" ><b>Lembre-se de deixar seu laboratório identico ao da Figura 03</b></p>

<p align="justify">É um curso gratuíto de 10 horas, que não tem obrigatoriedade de sua realização, mas já disponibiliza conteúdo e a o download da ferramenta. O mais importante é que você pode até achar o arquivo de instalação do Packet Tracer na internert, todavia para liberar todas as funcionalidades da ferramenta é necessário um login criado no cadastro deste curso, vou disponiblizar a seguir o arquivo para download direto que salvei no google drive:</p>


<h3 align="left">3 - Execução do Laboratório</h3>
<p align="justify">Conforme abordado no Item 1, o arquivo temporário de configuração de um roteador fica localizado na RAM, toda configuração que está sendo digitada e feita durante o laboratório encontra-se na RAM, salva em um arquivo chamado <b>running-config</b>, caso ocorra um desligamento do router ou switch, toda a configuração será perdida. </p>

<p align="justify">Para que a configuração feita não se perca, deve-se salvar seu conteúdo na NVRAM em um arquivo chamado <b>startup-config</b>, no qual a cada inicialização do Sistema Operacional (SO), esta configuração é carregada. O procedimento para salvar o conteúdo da RAM na NVRAM é através do comando <b>copy running-config startup-config</b>, devendo ser executado no prompt privilegiado.</p>

<p align="justify">Será seguida a seguinte sequência de configuração dos equipamentos:</p>

1. Configuração dos Switchs;
2. Configuração dos Clientes Debian; e,
3. Configuração do Router.

<p align="justify">Em algumas situações esta ordem não será seguida no roteiro, todavia será explicitado ao longo deste manual</p>

<h3 align="left">3.1 - Configuração dos Switchs</h3>

<p align="justify">As configurações necessárias para implentação de VLAN neste ambiente é a criação da vlan, e o modo como as portas estarão operado:</p>

* Modo Trunk - Quando na porta existe a necessidade de trafegar pacotes de mais de uma vlan;
* Modo Access - Quando na porta está trafegando <b>exclusivamente</b> pacotes de somente uma vlan.


<h3 align="left">3.1 - Configuração dos Switch ESW1</h3>

<p align="justify">Após concluir a configuração do desenho do ambiente, e linkar todos os dispositivos, inicialize os equipamentos com o botão Start (localizado logo abaixo do menu <b>Annotate</b>), ao dar dois cliques em cima do desenho do Switch ESW1 será aberto o prompt de configuração, e carregado o SO do equipamento conforme Figura 06.</p>
<p align="center"><img src="images/prompt.png"  width="700" height="464" align="middle"/></p>
<h4 align="middle">Figura 06 - Prompt Switch</h4>

<h2 align="middle">Criando Vlan</h2>
<p align="justify">Acesse o prompt de configuração com o comando <b>conf t</b>, acesse o prompt de configuração da vlan com o comando <b>vlan 10</b>, atribua o nome da vlan com o comando <b>name contabilidade</b>, por fim saia do prompt da interface com o comando <b>exit</b>, repita o procedimento para criar as outras 03 (três) vlans conforme apresentado na Figura 07: </p>
<p align="center"><img src="images/vlan-conf3.png"  width="480" height="196" align="middle"/></p>
<h4 align="middle">Figura 06 - Prompt Switch</h4>