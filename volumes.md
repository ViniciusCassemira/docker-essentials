# Volumes 💾📦

Agora que você sabe criar suas próprias imagens e seus containers, você se dá conta de que, quando um container é removido, todos os seus dados são excluídos juntos. Existe uma forma de persistir seus dados, conhecida como **volumes**.

Com volumes, é possível criar uma cópia dos dados do nosso container em nossa máquina (host). Assim, mesmo que o container seja removido ou pare de funcionar, teremos todos os seus dados salvos, podendo ser usados em novos containers.

Os principais tipos de volumes são:
✅ **Volumes Nomeados** – Criados com um nome específico, facilitando o gerenciamento.  
✅ **Volumes Anônimos** – Criados automaticamente sem um nome definido, geralmente usados para armazenamento temporário.

# Volumes Nomeados  
Esses possuem um nome definido pelo usuário, tornando-os fáceis de identificar, gerenciar e compartilhar entre containers. O Docker cria e gerencia volumes nomeados e armazena seus dados em um local específico do sistema do host. Geralmente, esse local fica no diretório de instalação do Docker, com um ID correspondente ao nome do volume. Oferecem maior controle e flexibilidade, pois é prático fazer referência a eles usando seus identificadores legíveis por humanos.

# Volumes Anônimos  
Já os volumes anônimos não possuem um nome definido pelo usuário. O Docker os cria automaticamente quando você cria um container e associa um ID exclusivo a esse volume. É mais difícil gerenciar esse tipo de volume devido à falta de um identificador legível por humanos. Seu uso é mais comum para armazenamento temporário, quando você apaga o coantainer esse volume continua existindo, mas como possui um nome aleatório é mais trabalhoso usá-lo novamente.

Conheça os comandos para manipular e criar volumes [clicando aqui](./commands.md).