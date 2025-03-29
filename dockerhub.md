# DockerHub
Imagine que você tenha desenvolvido uma imagem da sua aplicação a partir de um _Dockerfile_ e queira disponibilizá-la para que seu colega possa criar uma instância dessa imagem (container) na máquina dele. Talvez você esteja se perguntando como fazer esse compartilhamento ou como garantir que seu colega sempre tenha a versão mais atual da imagem. Para isso, existe uma solução simples e prática: o _DockerHub_.

O DockerHub é um dos principais _registros de imagens_ (Container Registry), funcionando como um repositório de código (como o GitHub ou GitLab), mas voltado para o armazenamento e a distribuição de imagens de contêiner. Nele, você pode baixar imagens já disponíveis para sua máquina e usá-las em seus projetos(como Nginx, MySQL e Node, por exemplo), além de criar suas próprias imagens e compartilhá-las com a comunidade.

Quando você faz o download de uma imagem que se encontra em algum Registro de imagem, você realiza um _Pull_, já quando faz o envio / atualização de uma imagem, essa ação é chamada de _Push_.

### Outros Registros de imagens são:
* Amazon Elastic Container Registry (ECR)
* Google Artifact Registry
* Azure Container Registry (ACR)
* GitHub Container Registry (GHCR)
* GitLab Container Registry
* Harbor
* JFrog Artifactory

Conheça os comandos para manipular as imagens do DockerHub [clicando aqui](./commands.md).