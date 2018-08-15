# Padrões Arquiteturais e Aplicações Corporativas

Os padrões arquiteturais propostos por Martin Fowler em seu livro **Patterns of Enterprise Application Architecture** servem como base/modelos de referência para a definição de classes e objetos em aplicações corporativas nos mais variados contextos.

Os padrões:

- **Web Presentation Patterns**: padrões de definição de classes e objetos voltados para separar a apresentação da lógica em aplicações web.
    - Model View Controller (MVC)
    - Page Controller
    - Front Controller 
    - Transform View
    - Two Step View
    - Application Controller 
- **Distribution Patterns**: padrões de definição de classes e objetos voltados para aplicações distribuidas (comunicação remota ou cliente-servidor). 
    - Remote Facade (Fachada Remota): Quando estamos trabalhando em aplicações distribuidas deveríamos evitar a realização de requisições consecutivas ao servidor, pois cada requisição tem um custo considerável sobre TCP/IP. Neste caso Fowler sugere a utilização de uma fachada remota com "métodos gordos" para orquestração e chamada a objetos pequenos de "métodos magros/finos". Requisitar a um "método gordo" não é uma boa ideia no domínio da aplicação, mas em requisições remotas é uma boa ideia. Neste caso o "método gordo" deve lidar com toda a complexidade e devolver a informação completa, evitando assim várias requisições consecutivas do cliente para o servidor.
    - Data Transfer Objet (DTO): padrão usado para transferir dados em aplicações distribuidas. No lado servidor o ideal é usar algum montador ou fábrica para montar/produzir os objetos de domínio com base no DTO recebido. 
- **Offline Concurrency Patterns**: padrões de definição de classes e objetos voltados para aplicações que lidam com concorrências.
    - Optimistic Offline Lock
    - Pessimistic Offline Lock
    - Coarse Graimed Lock
    - Implicit Lock
- **Session State Patterns**: padrões de definição de classes e objetos voltados para aplicações que precisam fazer tratamento de sessão.
    - Client Session State 
    - Server Session State 
    - Database Session State 
- **Base Patterns**: padrões de definição de classes e objetos básicos que podem ser usados em vários contextos.
    - Gateway: trata-se de uma classe que protege sua aplicação de mudanças externas. Pode ser usado no acesso a APIs de terceiros (criptografia, acesso a banco de dados, comunicação, dentre outros). Seus objetos devem acessar recursos externos ou de terceiros através deste Gateway, o que traduz as chamadas de método simples para a API especializada apropriada.
    - Mapper: a mesma ideia do Gateway.
    - Layer Supertype (Super Classe): trata-se de um objeto com métodos comuns na aplicação. Em vez de você duplicar métodos a ideia é transferi-los para uma super classe que pode então ser especializada ou compartilhada (se for estática).
    - Separated Interface (Interface Separada): a ideia é separar a implementação de uma interface de sua definição. Hoje isso é muito usado em conjunto com o padrão Repositório. A definição da interface fica na camada de domínio e a implementação da interface fica na camada de infraestrutura.
    - Registry: um registro é essencialmente um objeto global, ou pelo menos parece um - mesmo que não seja tão global como possa aparecer. Um registro serve para localizarmos algo neste registro.
    - Value Object (Objeto de Valor): um pequeno objeto simples, como dinheiro ou um intervalo de datas, cuja igualdade não é baseada na identidade.
    - Money 
    - Special Case (Herança): uma subclasse que fornece comportamento especial para casos específicos.
    - Plugin 
    - Service Stub (Serviço Stub): a ideia é colocar uma interface no meio do caminho entre sua aplicação e recursos de terceiros e utilizar no domínio da aplicação a interface e não a implementação diretamente. Quando fazemos isso podemos injetar um serviço falso (Mock) para a realização de testes ou um serviço temporário em caso de queda do serviço real.
    - Record Set (Conjunto de Registros): uma representação na memória dos dados tabulares.
- **Domain Logic Patterns**: padrões de definição de classes e objetos voltados para lidar com a lógica da aplicação (domínio da aplicação e objetos de domínio)
    - Transaction Script 
    - Domain Model (DDD)
    - Table Module: uma única instância que lida com a lógica de negócios para todas as linhas em uma tabela ou exibição de banco de dados.
    - Service Layer (Camada de Serviço): a ideia é levar a complexidade de acesso a operações que não fazem parte do domínio da aplicação para uma camada específica.
- **Data Source Architectural Patterns**: padrões de definição de classes e objetos voltados para aplicações que precisam lidar com acesso a dados.
    - Table Data Gateway: gateway para tabelas de banco de dados é um objeto que atua como um Gateway=Protetor/Intermediário para uma tabela de banco de dados. Uma instância lida com todas as linhas na tabela. Neste caso todo o SQL fica neste objeto, ou seja, ele abstrai a complexidade de lidar com instruções SQL.
    - Row Data Gateway 
    - Active Record: a ideia é deixar no próprio objeto de domínio comportamentos de acesso a dados. É comum encontrar este padrões em frameworks PHP.
    - Data Mapper: classes mapeadoras de classes para tabelas.
- **Object-Relational Behavioral Patterns**: padrões de classes e objetos voltados para melhorar o carregamento de outros objetos.
    - Unit of Work: mantém uma lista de objetos afetados por uma transação comercial e coordena a redação de mudanças e a resolução de problemas de concorrência. Muito usado hoje para controlar o acesso único a repositórios do Entity Framework. Neste caso o objeto DbContext fica com UnitOfWork que controla tudo. Na camada de dominio então acessamos o DbContext a partir de UnitOfWork. Isso é importante para evitar a criação de vários DbContexts na mesma transação.
    - Identity Map (Mapa de Identidade): garante que cada objeto seja carregado apenas uma vez, mantendo todos os objetos carregados em um mapa. Olha objetos usando o mapa quando se refere a eles.
    - Lazy Load (Carga Prequiçosa / Carregamento Tardio): um objeto que não contém todos os dados que você precisa, mas sabe como obtê-los. Muito usado hoje em frameworks ORM para o carregamento tardio de relacionamentos.
- **Object-Relational Structural Patterns**: padrões de definição de classes e objetos voltados para aplicações que acessam bases de dados relacionais.
    - Identity Field
    - Foreign Key Mapping
    - Association Table Mapping 
    - Dependent Mapping 
    - Embedded Value 
    - Serialized LOB (LOB Serializado): os objetos não precisam ser mantidos como linhas de tabela relacionadas entre si. Outra forma de persistência é a serialização, onde um gráfico inteiro de objetos é escrito como um único objeto grande (LOB) em uma tabela, este LOI serializado se torna uma forma de memento [Gang of Four].
    - Single Table Inheritance (Herança de Tabela Simples): a ideia é pegar uma tabela e gerar vários objetos relacionados.
    - Class Table Inheritance
    - Concrete Table Inheritance 
    - Inheritance Mappers 
- **Object-Relational Metadata Mapping Patterns**: padrões de classes e objetos voltados para acesso a dados.
    - Metadata Mapping 
    - Query Object (Objeto de Consulta): um objeto que representa uma consulta de banco de dados. Sempre usamos o LINQ do .NET Framework estamos usando objetos geradores de consulta.
    - Repository (Repositório): objeto que abstrai a complexidade de acesso a dados. Muito usado hoje para tirar da camada de domínio a complexidade de lidar com acesso a dados e para diminuir o acomplamento da camada de domínio com APIs de infraestrutura para acesso a dados.

--- 

**Fontes** 
- https://martinfowler.com/eaaCatalog/index.html
- https://www.devmedia.com.br/unit-of-work-o-padrao-de-unidade-de-trabalho-net/25811 (UnitOfWork por DevMedia)
- https://dotnetthoughts.net/implementing-the-repository-and-unit-of-work-patterns-in-aspnet-core/ (UnitOfWork por DotNetThoughts)