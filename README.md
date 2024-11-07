# NASA-Management_tasks
Sistema de gerenciamento de tarefas baseado em Python
## Sistema de Gerenciamento de Missões Espaciais

## 1. Descrição do Sistema

O **Sistema de Gerenciamento de Missões Espaciais** permite o gerenciamento de astronautas, equipes, missões, espaçonaves e problemas durante as missões. Através deste sistema, é possível:

- Adicionar astronautas e equipes.
- Criar e gerenciar missões.
- Associar espaçonaves às missões.
- Monitorar o progresso das missões e reportar problemas relacionados.

O sistema é construído utilizando o banco de dados **SQLite**, com o uso de **SQLAlchemy** como ORM (Object Relational Mapper) para manipulação dos dados.

## 2. Estrutura do Banco de Dados

O banco de dados é composto pelas seguintes tabelas, representadas pelas classes no código:

### **Astronauta**
- `id` (Integer, Primary Key): Identificador único do astronauta.
- `nome` (String): Nome do astronauta.
- `especialidades` (String): Especialidades do astronauta.
- `equipes` (Relationship): Relacionamento com a tabela **Equipe**, indicando a associação do astronauta a diferentes equipes.

### **Equipe**
- `id` (Integer, Primary Key): Identificador único da equipe.
- `astronauta_id` (Integer, Foreign Key): Identificador do astronauta associado à equipe.
- `nomeEquipe` (String): Nome da equipe.
- `missao_id` (Integer, Foreign Key): Identificador da missão associada à equipe.
- `missao` (Relationship): Relacionamento com a tabela **Missao**, indicando a missão atribuída à equipe.

### **Missao**
- `id` (Integer, Primary Key): Identificador único da missão.
- `nomeMissao` (String): Nome da missão.
- `lancamentoData` (Date): Data de lançamento da missão.
- `dataInicio` (Date): Data de início da missão.
- `dataFim` (Date): Data de fim da missão (se aplicável).
- `missaoAtiva` (Boolean): Indicador se a missão está ativa.
- `centro_controle_id` (Integer, Foreign Key): Identificador do centro de controle da missão.
- `espaconave_id` (Integer, Foreign Key): Identificador da espaçonave associada à missão.
- `equipe` (Relationship): Relacionamento com a tabela **Equipe**, indicando a equipe atribuída à missão.

### **Espaconave**
- `id` (Integer, Primary Key): Identificador único da espaçonave.
- `capacidade_carga` (Float): Capacidade de carga da espaçonave (em kg).
- `modelo` (String): Modelo da espaçonave.
- `statusProblema` (String): Status de problemas relacionados à espaçonave.

### **CentroDeControle**
- `id` (Integer, Primary Key): Identificador único do centro de controle.
- `nome` (String): Nome do centro de controle.
- `localizacao` (String): Localização do centro de controle.

## 3. Funções do Sistema

O sistema oferece várias funcionalidades acionadas por meio de um menu interativo no terminal. As opções disponíveis são:

- **Adicionar Astronauta**  
  Adiciona um astronauta ao sistema. Entrada: nome e especialidades.  
  Saída: Confirmação de que o astronauta foi adicionado com sucesso.

- **Remover Astronauta**  
  Remove um astronauta do sistema. Entrada: nome do astronauta.  
  Saída: Confirmação de que o astronauta foi removido.

- **Consultar Astronautas Cadastrados**  
  Exibe todos os astronautas cadastrados no sistema.  
  Saída: Lista com ID, nome e especialidades de cada astronauta.

- **Criar Equipe**  
  Cria uma nova equipe e atribui astronautas a ela.  
  Entrada: nome da equipe, nomes dos astronautas e nome da missão (opcional).  
  Saída: Confirmação de que a equipe foi criada com sucesso.

- **Listar Equipes**  
  Exibe todas as equipes criadas, com seus respectivos astronautas.  
  Saída: Lista de todas as equipes no sistema.

- **Criar Missão**  
  Cria uma nova missão e a associa a uma equipe.  
  Entrada: nome da missão e nome da equipe.  
  Saída: Confirmação de que a missão foi criada e associada à equipe.

- **Consultar Missões**  
  Exibe todas as missões registradas no sistema, com detalhes como nome, equipe responsável, e datas.  
  Saída: Lista de missões com informações detalhadas.

- **Consultar Participação em Missão**  
  Exibe os astronautas participantes de uma missão específica.  
  Entrada: nome da missão.  
  Saída: Lista de astronautas participantes.

- **Iniciar Missão**  
  Marca uma missão como iniciada.  
  Entrada: nome da missão.  
  Saída: Confirmação de que a missão foi iniciada.

- **Finalizar Missão**  
  Marca uma missão como finalizada.  
  Entrada: nome da missão.  
  Saída: Confirmação de que a missão foi finalizada.

- **Adicionar Espaçonave**  
  Adiciona uma nova espaçonave ao sistema.  
  Entrada: modelo da espaçonave e capacidade de carga.  
  Saída: Confirmação de que a espaçonave foi adicionada.

- **Lançar Espaçonave**  
  Associa uma espaçonave a uma missão ativa e registra o lançamento.  
  Entrada: nome da missão e modelo da espaçonave.  
  Saída: Confirmação do lançamento.

- **Monitorar Missão**  
  Exibe informações detalhadas sobre uma missão ativa, incluindo astronautas e status da espaçonave.  
  Entrada: nome da missão.  
  Saída: Informações detalhadas sobre a missão.

- **Reportar Problema**  
  Permite reportar problemas durante uma missão relacionados à espaçonave.  
  Entrada: nome da missão, nome da espaçonave e descrição do problema.  
  Saída: Confirmação do problema reportado.

## 4. Fluxo de Execução

O sistema inicia através da função `main()`, que exibe um menu com as opções disponíveis. Dependendo da escolha do usuário, a função correspondente é chamada e o processo é executado. O sistema continua até que o usuário opte por encerrar ou escolha uma opção inválida.

**Exemplo de fluxo de trabalho:**
1. O usuário escolhe a opção "Adicionar astronauta".
2. O sistema solicita o nome e as especialidades do astronauta.
3. O astronauta é adicionado à tabela **Astronauta** no banco de dados e uma mensagem de confirmação é exibida.

## 5. Como Usar

1. Execute o script Python. Certifique-se de ter o **SQLAlchemy** instalado em seu ambiente:
   ```bash
   pip install sqlalchemy
   ```
2. Após iniciar o script, um menu será exibido com opções numeradas. Digite o número correspondente à ação desejada.
3. O sistema solicitará as informações necessárias, como nome de astronauta, equipe, missão, etc.
4. O sistema exibirá mensagens de confirmação ou erro conforme o caso.
5. Para sair do sistema, basta interromper a execução do script (Ctrl+C no terminal).

## 6. Conclusão

Este sistema oferece uma maneira simples e eficaz de gerenciar missões espaciais, astronautas, equipes, espaçonaves e problemas durante o processo. Utilizando **SQLAlchemy** para interagir com o banco de dados, o sistema permite fácil expansão e personalização. A estrutura do banco de dados está organizada para facilitar a adição de novas funcionalidades no futuro.
