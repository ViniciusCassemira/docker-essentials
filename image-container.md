# Containers e Imagens 📦🖼️

Afinal, o que é uma **imagem** e qual é sua diferença em relação a um **container**?

Imagine que você terminou de desenvolver a sua aplicação, e deseja utilizar o Docker para instanciá-la em diferentes ambientes e máquinas. Como você já deve ter visto, será preciso criar um arquivo **Dockerfile** em seu projeto, passando nele todas as informações necessárias para a criação da imagem. Você passa uma imagem base, quais arquivos devem ser usados, os comandos de inicialização, variáveis, até que aconteça o build e sua imagem fique pronta.

Uma imagem nada mais é do que uma versão totalmente pronta e usável, seja de uma aplicação ou tecnologia. Ela é imutável, ou seja, uma vez criada, **não pode ser modificada**. Caso seja necessário modificar algo, **uma nova imagem deve ser gerada**.

Imagine uma imagem como uma planta baixa imutável de uma casa, onde são informadas as medidas, a quantidade de cômodos e todas as informações necessárias. Um container seria a implementação da casa a partir dessa "planta baixa", onde todos os atributos para a sua construção são usados. **Vários containers podem ser criados e usados simultaneamente a partir de uma mesma imagem**, pois tratam de implementações isoladas e independentes.

Você pode, por exemplo, baixar uma imagem do **MySQL** em sua máquina, e a partir dessa imagem, criar **várias instâncias** (ou containers) e usar cada uma em um projeto diferente. Fazendo uma analogia com programação orientada a objetos, _imagine a imagem sendo uma classe, enquanto os containers seriam objetos dessa classe._

Conheça os comandos para criar e gerenciar imagens e containers [clicando aqui](./commands.md).