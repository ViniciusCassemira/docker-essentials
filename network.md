# Networks 🌐🔗
No Docker, as redes(networks) são utilizadas para conectar os containers com seu host e com outros containers no mesmo host.
**Obs:**Quando utilizamos kubernetes, esse conceito de network não se aplica, lá utilizamos o conceito de _services_.

Por padrão, quando você cria um container no Docker sem especificar uma rede personalizada, **ele é atribuído automaticamente à rede bridge**, que é a rede padrão do Docker. A partir dessa configuração, os containers podem se comunicar entre si através de IPs, mas **não conseguem se resolver pelo nome do container**, que é algo que normalmente acontece quando você usa redes personalizadas do Docker.

## Principais tipos de network
O Docker possui diversos tipos de redes, cada um com um propósito e casos de uso diferentes

### Bridge
É a rede padrão dos containers quando nenhuma network é especificada. É criado uma rede isolada para os containers, permitindo que enxerguem outros containers na mesma rede somente através de seu IP, para serem acessados fora da Bridge, o mapeamento de portas é necessário.

### None
Esse tipo de rede isola os containers de seu host e de todos os seus componentes (outros containers existentes), desativando qualquer conectividade de rede do container inserido nessa network.

### Host
Na rede host, o isolamento de rede entre o container e o host é removido, fazendo com que o container utilize o IP do host diretamente. Isso significa que o container não precisa de um mapeamento de portas para ser acessado, já que ele compartilha a mesma interface de rede do host. Containers nessa rede só conseguem se conectar a aplicações ou containers que também estejam expostos na rede do host, que tenham mapeamentos de portas configurados no host.

## Outros tipos de networks:
**Overlay**: Usado em ambientes distribuídos com vários hosts Docker. Permite que containers em diferentes nós se comuniquem como se estivessem na mesma rede local, sendo comum em arquiteturas de orquestração como o _Docker Swarm_.

**IPvlan**: Permite que containers tenham endereços IP diretamente na rede física, sem precisar de NAT. Isso melhora o desempenho e a compatibilidade com redes empresariais.

**Macvlan**: Cria interfaces de rede virtuais para os containers, permitindo que eles sejam tratados como dispositivos físicos na rede. Isso facilita a comunicação direta com outros dispositivos sem passar pelo host.

Conheça os comandos para gerenciamento de redes [clicando aqui](./commands.md)