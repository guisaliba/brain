# subject: [[docker]]
# topics: #docker #containers #vm

## A palavra chave para entender o Docker é **containers.**

Entender o que são os containers é fundamental para entender o funcionamento do Docker.

E para entendermos os containers, precisamos entender o conceito de **máquinas virtuais.**

Uma máquina virtual é um ambiente que roda dentro de outro Sistema Operacional (**OS**). Ela emula um Sistema Operacional inteiro, desde o Kernel até todas as configurações do OS escolhido. Isso faz com que o usuário tenha um **overhead** de recursos.

E o que significa um overhead de recursos? Significa que, quando uma máquina virtual é inicializada, ela vai obrigatoriamente sequestar recursos da máquina em que ela está hospeadada.

Isto é, processamento de CPU e memória dispónível. Quanto mais máquinas virtuais inicializadas, ou seja, quanto mais ambientes sequestrando recursos, mais pesado todo o processo fica.

Essas máquinas poderiam ser utilizadas por exemplo, em uma aplicação escalonável, que cresce cada vez mais de tamanho, demandando cada vez mais máquinas virtuais levantadas. A partir disso, torna-se necessário um ambiente leve, simples e propício: **************os containers.**************

## Os containers:

Ao invés de virtualizar uma máquina inteira para criar um novo ambiente, os containers são apenas um processo no OS que é ****************enganado****************, por achar que ele possui um Sistema Operacional inteiro à sua disposição. No fim, ele é apenas um processo, muito mais simples, eficiente e barato.

Essa é a ideia do **Docker**. Criar containers para construir aplicações dentro deles. A principal vantagem dos containers é que, diferente das máquinas virtuais, eles compartilham recursos com o OS principal, e compartilham também entre si (no caso de vários containers rodando na máquina).