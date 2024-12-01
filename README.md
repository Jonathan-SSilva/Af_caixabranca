**Erros que podem conter no código: **

- [ ] Erro na inicialização do driver JDBC,
- [ ] URL de conexão inválida,
- [ ] Conexão não tratada adequadamente,
- [ ] Vulnerabilidade de SQL Injection,
- [ ] Não fechar recursos,
- [ ] Tratamento de exceções vazio,
- [ ] Conexão pode ser nula,

Alguns desses erros podem sem muito comuns nesse tipo de codigo.

**Erros no código:**

(Class.forName("com.mysql.Driver.Manager").newInstance();)

- O nome da classe sendo instanciada pra conectar com o banco "com.mysql.Driver.Manager" está errada, deveria ser "com.mysql.cj.jdbc.Driver"

(String url = "fdbc:mysql://127.0.0.1/test?=user=lopes&password=123";)

- A URL de conexão contém erros de sintaxe:  
- O prefixo correto para MySQL é jdbc:mysql://

(sql += "select nome from usuarios ";
sql += "where login = " + "'" + login + "'";
sql += " and senha = " + "'" + senha + "';";)

- Concatenar valores diretamente na query é extremamente inseguro, pois permite ataques de SQL Injection.

(Statement st = conn.createStatement();
ResultSet rs = st.executeQuery(sql);)

- Recursos como Statement, ResultSet, e Connection não são fechados, o que pode causar vazamento de recursos.

(Connection conn = DriverManager.getConnection(url);)
O método conectarDB() não está tratando adequadamente a conexão:

- Não há tratamento de exceções para exibir informações úteis ao desenvolvedor.
- A conexão não é fechada ao final do processo.


**Testes:**

Teste de estrutura de controle

Cenário 1: O banco de dados está acessível, e o login e senha correspondem a um usuário válido.
Cenário 2: O banco de dados está acessível, mas o login ou senha estão incorretos.
Cenário 3: O banco de dados está inacessível (erro na conexão).
Cenário 4: A conexão foi feita, mas a tabela ou campos esperados não existem (erro na query).:

- Certo, todos os trechos de código são executados.

Teste de condição:

C1: O banco de dados está acessível (conn != null).
C2: O banco de dados não está acessível (conn == null).
C3: O ResultSet contém registros (rs.next() == true).
C4: O ResultSet está vazio (rs.next() == false).

Certo.

-  if (rs.next())
    - rs.next() = true
    - rs.next() = false

Teste de fluxo de dados:

- Connection conn = null;
- String url = "fdbc:mysql://127.0.0.1/test?=user=lopes&password=123";
- public String nome = "";
- public boolean result = false;
- String sql = "";
- Connection conn = conectarDB();
- Statement st = conn.createStatement()
- ResultSet rs = st.executeQuery(sql);

Certo, todas as variáveis são declaradas antes do uso, e todas são utilizadas.

Teste de ciclo:

Certo, No código não há estruturas explícitas de repetição.


Grafo de Fluxo:
![Image](https://github.com/user-attachments/assets/70b3e69e-562a-4e5d-933f-615a386b41e2)


Complexidade ciclomática (M)

M = E - N + 2P

E (arestas) = 13

N (nós) = 9

P (componentes conectados) = 2

M = 13 - 9 + (2*2)

M = 4 + 4 = 8

Caminhos possíveis

4-1-3-5-6-9

4-1-2-3-5-8-9

4-1-3-5-6-8-9

4-1-3-5-6-7-8-9

4-1-3-5-8-9

4-1-3-5-6-7-9
