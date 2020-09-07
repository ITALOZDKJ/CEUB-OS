Objetivo, primeiros passos para iniciar a produção da distribuição CEUB-OS:

Pré-requisitos
   1. Debian
   2. Versão atualizada do Live-build
   3. Bash
   4. Internet
   5. 100GB de disco disponível no seu sistema Linux instalado e máquina física ou máquina Virtual. 8GB de RAM.

Licença de uso
O linux utiliza a licença GPL, o que permite a qualquer um criar um remaster ou distribuição própria. É necessário preocupar-se com as licenças de software que você irá usar em seu sistema.

Drivers proprietários
Nunca instale drivers proprietários em seu remaster. Por padrão pode ocorrer diversos erros, sendo assim, o ideal é que o usuário final instale esses drivers caso necessário.

Qual Debian utilizar?
É recomendado utilizar a versão Stable do Debian.

Distribuição ou Remasterização.
Normalmente uma remasterização tem uma finalidade específica para um público específico. Exemplo: Uma distro para sua empresa com as ferramentas de uso padrão.
Já uma distribuição, tem um público maior (usuário final), neste caso você precisa pesquisar por programas que serão adicionados, personalização de interface, configuração de repositório e etc…

Live Build
Live-Build é criado pela própria comunidade Debian. Sendo um conjunto de scripts para criar imagens do sistema live.

O que tem em uma imagem live?
    • Imagem do kernel linux - Geralmente chamada de vmlinuz
    • Imagem do disco RAM inicial - initrd (O live build cria esta etapa)
    • Imagem do sistema (Squashfs) é uma compactação da imagem - Sendo somente leitura.
    • Bootlooader - Software para iniciar e selecionar um kernel e outras opções.

Download e instalação do Debian
Debian - versão mínima (netinstall)
Link direto para download:
https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-10.5.0-amd64-netinst.iso
Instalar em uma máquina virtual - Recomendo: Virtualbox.
Coloca entre 30 e 50GB de HD virtual - Em rede, coloca em modo bridge - na instalação do Debian, em seleção de software, deixe marcado apenas:
    • Utilitário de sistema padrão
    • Servidor SSH
Verifique o IP da máquina virtual instalada e para facilitar as ações (como ter opção de copiar e colocar) acesse esta máquina via SSH, exemplo:

# ceubos-core
CeubOS Core Team 


# Atualizar seus repositorios para o backports
\</etc/apt/sources.list\> \
deb http://deb.debian.org/debian buster-backports main contrib non-free \
deb-src http://deb.debian.org/debian buster-backports main contrib non-free 

Apos isso, atualizar os seus repostorios e a maquina
`sudo apt update && sudo apt upgrade`


# Instalar as dependencias
`sudo apt install live-build live-manual live-config schroot`

# Compilar sua primeira versao
1. Clone o repositorio para sua maquina \
`git clone https://github.com/francisco-pc7063/ceubos-core.git`
2. Va para o diretorio que possui as instrucoes do live build \
`cd ./ceubos-core/live`
3. Dentro do repositorio, ha um script chamado **live.sh** executeu e depois mande o live-build construir a iso
```
./live.sh
sudo lb build
```
4. Se o live-build conseguir executar sem erros, sera criado um arquivo chamado **live-image-amd64.hybrid.iso**
Para executar novamente, sera necessario excluir o atual e buildar novamente:
```
sudo lb clean --all
./live.sh
sudo lb build
```
# Referencias
https://live-team.pages.debian.net/live-manual/html/live-manual/about-manual.en.html
