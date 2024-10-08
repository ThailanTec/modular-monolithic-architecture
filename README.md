# modular-monolithic-architecture

# O que é Arquitetura Monolítica Modular?

Na arquitetura monolítica tradicional, toda a aplicação é um único bloco (monólito) onde todas as funcionalidades estão juntas e dependem umas das outras. Já na arquitetura monolítica modular, a ideia é dividir essa aplicação monolítica em módulos independentes, que seguem regras bem definidas, como se fossem componentes separados.

Esses módulos se comunicam entre si através de interfaces claras (métodos, contratos) sem depender diretamente do código de outros módulos. Isso traz uma organização mais limpa e facilita a evolução e a manutenção da aplicação.

Combinando isso com o DDD (Domain-Driven Design), você estrutura sua aplicação em torno de domínios de negócio (módulos), cada um com suas próprias responsabilidades bem definidas, isolando a lógica de negócio em diferentes camadas e mantendo uma separação clara entre o que pertence ao domínio e outras partes da aplicação (ex.: infraestrutura, banco de dados, interfaces, etc.).
Organização de um Projeto Go com Monolito Modular e DDD

A ideia principal é que os módulos representem diferentes contextos de negócio. No DDD, esses módulos podem ser representados por Bounded Contexts (Contextos Delimitados), que são as partes autônomas da aplicação.

``` .
├── cmd
├── infra
│   └── database
├── internal
│   ├── auth
│   │   ├── domain
│   │   ├── interfaces
│   │   ├── repository
│   │   └── service
│   ├── order
│   │   ├── domain
│   │   ├── interfaces
│   │   ├── repository
│   │   └── service
│   └── user
│       ├── domain
│       ├── interfaces
│       ├── repository
│       └── service
├── pkg
└── utils
```

## Explicação dos Componentes

- cmd/app: Ponto de entrada da aplicação. Aqui você tem o main.go que inicializa tudo e executa o servidor.

- internal: Contém os módulos organizados por domínio. Cada módulo (ex.: user, order, payment) tem suas próprias pastas para entidades de negócio, casos de uso, interfaces (handlers/controllers) e repositórios. Isso garante que a lógica de negócio esteja isolada e separada de outras partes da aplicação.

- infra: Parte de infraestrutura onde você configura coisas como banco de dados, mensageria (Kafka, RabbitMQ, etc.), autenticação, cache, etc.

- pkg: Pacotes utilitários que podem ser compartilhados entre os módulos, como helpers, middlewares ou funções comuns.

## Vantagens

- Organização clara: Cada domínio (módulo) tem uma responsabilidade bem definida, facilitando a manutenção e evolução do sistema.
    
- Facilidade de refatoração: Por serem módulos isolados, é mais fácil alterar ou reescrever partes da aplicação sem impactar outros módulos.
    
-Melhor escalabilidade: Embora ainda seja um monólito, os módulos permitem que você escale partes específicas da aplicação ou que, eventualmente, migre módulos para microsserviços.
    
- Facilita a implementação de DDD: Fica mais fácil aplicar os conceitos de agregados, entidades, repositórios e serviços de domínio.

- Menor Complexidade: Diferente de microsserviços, não há necessidade de lidar com comunicação entre serviços, versionamento de APIs, ou orquestração complexa, o que simplifica a operação.

## Desvantagens

- Ainda um Monólito: Mesmo modularizado, é um único deploy. Se algo der errado, toda a aplicação pode ser afetada.

- Tamanho da Aplicação: À medida que o sistema cresce, o monólito modular pode ficar grande demais, exigindo mais recursos e tempo de build/deploy.

- Dependências Implícitas: Embora modularizado, ainda pode haver acoplamento entre módulos se não houver disciplina na separação de responsabilidades.
    
- Transição Complexa para Microsserviços: Caso o sistema precise ser migrado para microsserviços no futuro, mesmo com a modularidade, pode haver desafios na extração de módulos para serviços independentes.