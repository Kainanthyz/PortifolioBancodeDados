## 2° Semestre • 2022-2
#### PRO4Jobs
<p>Parceiro Acadêmico: <a href="https://www.pro4tech.com.br/">PRO4TECH</a></p>
<p align = "center"><img src= "imagens/logo2sem.png" width="250" height="250"></p>
<p>PRO4Jobs é uma aplicação desenvolvida para desktop e tem como principal intuito ajudar no controle e gerenciamento de vagas de emprego. O candidato realiza sua autenticação e pode encontrar, analisar e se canditar a vagas de emprego que possui interesse. Por outro lado, o RH consegue analisar os currículos dos candidatos para uma determinada vaga, além de poder aprovar ou reprovar os mesmos. </p>

## Tecnologias Utilizadas

* __Java:__ Linguagem de programação back-end;
* __Java Swing:__ Conjunto de bibliotecas da linguagem Java, utilizado para construção de interfaces gráficas de usuário (GUIs);
* __MySQL:__ Sistema Gerenciador de Banco de Dados utilizado para armazenar os dados provenientes da aplicação desenvolvida.
<br><br>

## Contribuições Pessoais
### Cadastro de vagas de emprego
<p>Esta é uma das principais funcionalidades da aplicação, pois é necessário o cadastro de vagas de emprego para que os candidatos possam analisá-las e se candidatarem. A responsabilidade da criação de uma vaga de emprego é do RH da empresa, que deverá detalhar os componentes que fazem parta da mesma. Entre os campos que uma vaga de emprego deve possuir temos, o nome, uma breve descrição, pretensão salarial, cargo e experiência necessária que o candidato deve ter.  </p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para criar uma nova vaga de emprego, foi necessário compreender a estrutura das tabelas do banco de dados desenvolvido, além de possuir um conhecimento básico da linguagem de programação Java. Primeiramente, no banco de dados, foi criada uma nova tabela destinada a armazenar as informações relacionadas à vaga de emprego. Em seguida, foi desenvolvida uma classe em Java que funciona como um Data Transfer Object (DTO) para armazenar temporariamente os dados da vaga.

Após isso, uma nova classe em Java foi criada para inserir registros dentro do banco de dados. Dentro desta classe, foi implementado um método específico que chama outro método de outra classe para estabelecer a conexão com o banco de dados. Depois, um comando SQL foi escrito para cadastrar as vagas de emprego no banco. As informações sobre a vaga de emprego são coletadas por meio de uma interface gráfica (GUI). Esta interface coleta os dados e os passa para a classe que armazena temporariamente essas informações.

A classe que contém o método de cadastro de vagas no banco então coleta os dados do DTO e os incorpora ao comando SQL. Finalmente, este método executa o comando no banco de dados, criando a nova vaga de emprego. Este processo garante que as vagas sejam inseridas corretamente e de maneira eficiente no sistema, facilitando o gerenciamento e a manutenção das informações sobre as oportunidades de emprego disponíveis.  </p>
<p>Abaixo é mostrado o método utilizado para inserir uma vaga de emprego no banco de dados: </p>

  ``` java
    public class VagaDAO {
            Connection conn;
            PreparedStatement pstm;

            public void cadastrarvaga(Vaga obj_cadastro_vaga){
            
            String sql = "insert into vaga(nome_vaga, descricao_vaga, pretencao_salarial, cargo, experiencia_profissional_necessaria, quantidade_candidatos, status) values (?, ?, ?, ?, ?, ?, ?)";
            conn = new ConexaoDAO().conectaBD();
            
            try {
                
                pstm = conn.prepareStatement(sql);
                
                pstm.setString(1,obj_cadastro_vaga.getNome());
                pstm.setString(2,obj_cadastro_vaga.getDescricao());
                pstm.setDouble(3,obj_cadastro_vaga.getSalario());
                pstm.setString(4,obj_cadastro_vaga.getCargo());
                pstm.setString(5,obj_cadastro_vaga.getExpe_prof());
                pstm.setInt(6, 0);
                pstm.setString(7, "ABERTA");
                pstm.execute();
                pstm.close();
                
                JOptionPane.showMessageDialog(null, "Vaga Cadastrada");
                
                
            } catch (SQLException erro) {
                JOptionPane.showMessageDialog(null,"VagaDAO: Cadastrar" + erro);
            
            }
        }
     }
  ```
</details>
<br>

### Criação de Banco de Dados
<p>Como a aplicação possui dados que não podem ser perdidos, foi necessário a construção de um banco de dados relacional. O banco de dados relacional consiste no armazenamento de dados em estruturas que se chamam tabelas, cada tabela deve possuir um identificador único (chave primária), que se trata de um valor que não pode se repetir mais de uma vez, e suas respectivas colunas. Além disso, as tabelas podem ter ligações entre si, e com base nessas relações pode ser necessário a criação de novas tabelas ou a adição de chaves estrangeiras.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para a criação de um banco de dados relacional, foi preciso escolher um SGBD (Sistema Gerenciador de Banco de Dados) que melhor se encaixesse no projeto que foi desenvolvido. O SGBD escolhido foi o MySQL, por se tratar de uma ferramenta simples e fácil de implementar. Após a escolha do SGBD, foi observado a modelagem de dados criada do projeto, porque com ela é criado o script do banco de dados. Em seguida, foi preciso criar um database, onde foi armazenado o banco de dados, depois foram criadas as tabelas e suas respectivas relações. O comando para criar tabelas no MySQL é o "CREATE TABLE", cada coluna deve ter seu nome e o seu tipo de dado que deve ser armazenado (inteiro, texto etc), além de uma chave primária e chave estrangeira (dependendo da relação da tabela com as outras).</p>
  <p>Abaixo é mostrado a criação de uma tabela no banco de dados do projeto:</p>

  ```sql
      create database banco;
      use banco;

      create table candidato(
          cpf varchar(14) not null,
          nome_completo varchar(50) not null,
          data_nascimento date not null,
          email varchar(30) not null,
          telefone bigint not null,
          endereco varchar(60) null,
          pretencao_salarial numeric(7,2) null,
          arquivo blob null,
          senha varchar(3000) not null,
          primary key (cpf)
    );
  ```
</details>
<br>

### Progresso do Candidato
<p>Após um candidato se candidatar a uma vaga de emprego, ele deve ser capaz de visualizar o seu progresso. Isso o ajuda a entender como ele está progredindo em uma determinada vaga. Por sua vez, o RH deve aprovar ou reprovar este candidato, caso seja reprovado, o RH deve enviar um motivo do porque o candidato foi reprovado. Após a reprovação ou aprovação do candidato, ele terá a transparência de ver este retorno.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>Para implementar a funcionalidade, deve-se ter uma relação entre as tabelas de Candidato e Vaga. Por meio da modelagem de dados foi entendido que as tabelas Candidato e Vaga tem relação entre si, sendo que nenhum ou muitos candidatos podem se candidatar a uma vaga e uma vaga pode ser concorrida por nenhuma ou muitas pessoas. Com base neste tipo de relação, foi necessário criar uma nova tabela contendo as chaves primárias da tabela de Candidato e Vaga, essas mesmas chaves são também ao mesmo tempo chaves estrangeiras. Foi necessário criar um método em Java, que faz a conexão com o banco de dados e altera as colunas status da vaga e motivo, dependendo se o candidato foi aprovado ou reprovado na vaga. Este método chama outro método de uma outra classe para fazer a conexão com o banco de dados e em seguida é executado uma consulta para poder coletar todas as vagas que um determinado candidato se candidatou. O resultado da consulta é armazenada dentro de uma lista, que depois é transferida para uma tabela da interface gráfica, sendo finalmente exibida ao candidato. </p>
  <p>Abaixo é mostrado como é realizada a consulta das vagas relacionadas a um determinado candidato:</p>

  ```java
      public ArrayList<Candidato_Vaga> MostrarVagas(Candidato objcandidato){
        
        String sql = "select v.nome_vaga,cv.status_vaga,cv.motivo from vaga as v "
                + "inner join candidato_vaga as cv on v.id_vaga = cv.fk_id_vaga "
                + "inner join candidato as cand on cand.cpf = cv.fk_cpf where cpf = ?";
        
        conn = new ConexaoDAO().conectaBD();
        
        try{
            pstm = conn.prepareStatement(sql);
            pstm.setString(1, objcandidato.getCPF());
            ResultSet rs = pstm.executeQuery();
            
            while (rs.next()){
                Candidato_Vaga objcv = new Candidato_Vaga();
                objcv.setNome_vaga(rs.getString("nome_vaga"));
                objcv.setStatus(rs.getString("status_vaga"));
                objcv.setMotivo(rs.getString("motivo"));
                lista.add(objcv);
                
            }
           
            
        } catch(SQLException e){
            JOptionPane.showMessageDialog(null, "CandidatoDAO: MostrarVagas" + e);
            return null;
        }
        return lista;
    }
    
    public ResultSet LoginCandidato(Candidato objcandidato){
        String sql = "select * from candidato where cpf = ? and senha = MD5(?)";
        conn = new ConexaoDAO().conectaBD();
        
        try {
            pstm = conn.prepareStatement(sql);
            pstm.setString(1, objcandidato.getCPF());
            pstm.setString(2,objcandidato.getSenha());
            ResultSet rs = pstm.executeQuery();
            return rs;
        } catch(SQLException erro){
            JOptionPane.showMessageDialog(null, "CandidatoDAO" + erro);
            return null;
        }
        
    }
  ```
</details>
<br>

<hr></hr>
<br><br>

## Aprendizados
<p>Durante o desenvolvimento do projeto, eu tive o papel de Product Owner, ou seja, tive a função de dialogar constantemente com o cliente parceiro, para esclarecer as dúvidas da equipe, além de mostrar como estava o andamento do projeto. Também tive o papel de levantar os requisitos que deveriam ser desenvolvidos após a reunião de kick-off com o cliente.</p>
<p>Ao mesmo tempo em que fui PO, também atuei na área de desenvolvimento. Fui responsável pela a elaboração do script de criação do banco de dados da aplicação, além de desenvolver as telas e realiazar a conexão entre o back-end e o banco de dados. Pude aperfeiçoar meus conhecimentos na linguagem Java, principalmente na questão de conexão e manipulação do Banco de Dados. Aprendi também a ser mais comunicativo e gerir o tempo de forma adequada para que todas as atividades fossem entregadas dentro do prazo estipulado. </p>

<br>

<h3 align = "center">Hard Skills</h3>

<table align="center">
    <tr>
      <th width="300px">Tecnologia/Metodologia</th>
      <th width="300px">Classificação</th>
    </tr>
    <tr>
      <td>Desenvolvimento de scripts SQL (SGBD MySQL)td>
      <td>Sei fazer com Autonomia</td>
    </tr>
    <tr>
      <td>manipulação e consulta de Banco de Dados, utilizando Java</td>
      <td>Sei fazer com Autonomia</td>
    </tr>
    <tr>
      <td>Java Swing</td>
      <td>Sei fazer com Autonomia</td>
    </tr>
    <tr>
      <td>Modelagem de Dados</td>
      <td>Sei fazer com Autonomia</td>
    </tr>
</table>

<h3 align = "center">Soft Skills</h3>

<table align="center">
    <tr>
      <th width="300px">Habilidade</th>
      <th width="300px">Descrição</th>
    </tr>
    <tr>
      <td>Organização</td>
      <td>Precisei me organizar para realizar o priorização do backlog do produto</td>
    </tr>
    <tr>
      <td>Trabalho em Equipe</td>
      <td>Precisei trabalhar em equipe para que as entregas fossem entregues com uma alta qualidade</td>
    </tr>
    <tr>
      <td>Gestão de Tempo</td>
      <td>Precisei gerenciar meu tempo para entregar as atividaes no prazo estipulado</td>
    </tr>
    <tr>
      <td>Inteligência Emocional</td>
      <td>Precisei controlar minhas emoções para que meu emocional não atrapalhasse meu desempenho</td>
    </tr>
</table>

<hr></hr>
<br>
