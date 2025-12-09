# 6° Semestre • 2025-2

<p align="center">
    <img width="1584" height="396" alt="image" src="https://github.com/user-attachments/assets/946d376d-f58b-41e7-b7e8-f45ea865d310" />

</p>

### Em 2025-2

Repositório: <a href="https://github.com/QuantumBitBR/API_6SEM">Clique aqui</a>

## 📝 Sobre

#### **Desafio**
O sistema de chamados acabou se tornando um ponto de atraso, já que muitos tickets eram recorrentes e abordavam problemas que já tinham sido solucionados, o que gerava retrabalho e consumia tempo da equipe. Isso comprometia a agilidade do suporte e dificultava a identificação de padrões, pois as informações permaneciam dispersas. Por isso, tornou-se importante adotar uma forma mais eficiente de organizar essas solicitações, reduzindo o esforço do time e permitindo uma gestão mais rápida e confiável das ocorrências repetidas.

#### **Solução Desenvolvida**  
A HelpAI foi criada como uma solução inteligente para otimizar a gestão de suporte e tornar as operações de atendimento ao cliente mais eficientes e estratégicas. Ela reúne recursos avançados que facilitam a análise de informações, garantem segurança dos dados e tornam o processo de tomada de decisão mais assertivo.

- **Busca avançada de tickets:** permite localizar chamados com rapidez e precisão.
- **Geração automática de insights estratégicos:** identifica padrões e oportunidades de melhoria.
- **Dashboard interativo:** oferece visualização clara e dinâmica dos principais indicadores.
- **Análise de tendências com IA:** interpreta o histórico de forma inteligente para revelar comportamentos e recorrências.
- **Anonimização de dados com conformidade LGPD:** assegura proteção e privacidade total das informações.
- **Relatórios automáticos com IA:** gera análises detalhadas e documentos completos de forma inteligente, reduzindo trabalho repetitivo.

Ao longo do tempo, o histórico de atendimento se transforma em uma fonte valiosa de inteligência corporativa, permitindo melhorias contínuas, maior eficiência operacional e decisões de negócio mais inteligentes.

Contribuições Pessoais
- Durante o projeto atuei como desenvolvedor focando no beck-end:

    - Requisições rest pelo python:
         A maior parte das requisições pelo python e end-points foram feitos por mim, nos ainda não tinhamos experiencia com um back-end com python entçai eu comecei a montagem dele e as divisões de pasta e arquivos
      ```python
      def get_user_by_id(self, userid):
        response = self.user_repository.get_by_id(userid)
        
        if response == None:
            return {
                "error": "User not found"
            }, 404

    - Filtros dos endpoint referentes as requisições de tickets:
      ```python
      def _build_where_clause_and_params(
        self,
        company_id: Optional[List[int]] = None, 
        product_id: Optional[List[int]] = None, 
        category_id: Optional[List[int]] = None, 
        priority_id: Optional[List[int]] = None, 
        createdat: Optional[str] = None,
        end_date: Optional[str] = None
        ) -> Tuple[str, List[Any]]:
            """
            Constrói a cláusula WHERE e a lista de parâmetros para a consulta SQL.
            Ajustado para usar 'IN' para listas de IDs.
            """
            conditions = []
            params = []
        
        id_filters = {
            'companyid': company_id,
            'productid': product_id,
            'categoryid': category_id,
            'priorityid': priority_id,
        }
        
        for col_suffix, ids in id_filters.items():
            if ids is not None and ids:
                conditions.append(f"t.{col_suffix} IN %s")
                params.append(tuple(ids))
                
        if createdat is not None:
            conditions.append("t.createdat >= %s")
            params.append(createdat)
            
        if end_date is not None:
            conditions.append("t.createdat <= %s")
            params.append(end_date)

        sql_where = " WHERE " + " AND ".join(conditions) if conditions else ""
        
        return sql_where, params
    A ideia dos filtros é prepará-los antes das requisições e depois chamá-los dentro da requisição, deixando os valores novos como opcionais, conseguindo assim aplicar filtros dentro da query do banco de dados.

# Aprendizados

## Hard Skills

| Habilidade               | Por que foi importante? |
|--------------------------|-------------------------|
| **Python** | Usei Python como base do backend e o microframework Flask para construir as APIs do sistema. Implementei rotas, regras de negócio e integrações necessárias para suportar as funcionalidades do projeto. | 
| **Elastic Search** | Ferramenta utilizada no desenvolvimento do projeto, com alto nível de proficiência na customização do ambiente e uso de plugins. | 
| **PostgreSQL** | Utilizei PostgreSQL no armazenamento estruturado dos dados, organizando tabelas, relacionamentos e garantindo consistência das informações utilizadas pelo backend. | 
| **VueJS** | Desenvolvi telas e componentes no front-end usando Vue.js, incluindo a interface do chatbot e outras áreas do sistema. Trabalhei com comunicação via API, estados reativos e usabilidade. |
| **Git/GitHub** | Utilizei Git para versionamento e GitHub para gerenciar o repositório do projeto, realizando commits, branchs, pull requests e colaborando com o time durante o desenvolvimento. |
| **Figma** | Participei da construção e validação das telas no Figma, garantindo que o design refletisse a experiência desejada e servisse como base visual para o desenvolvimento. |
| **Jira** | Utilizei o Jira para organizar tarefas, registrar histórias, acompanhar entregas e manter o fluxo de trabalho alinhado ao Scrum utilizado pela equipe.|

## Soft Skills

| Habilidade               | Por que foi importante? |
|--------------------------|-------------------------|
| **Comunicaçã** | Mantive alinhamento constante com o time e com o cliente, garantindo entendimento claro dos requisitos, priorizações e expectativas em cada etapa do desenvolvimento e também nas cerimônias do Scrum, como: Daily, Review, Retrospectiva e Planning. | 
| **Trabalho em equipe** | Atuei de forma colaborativa com os desenvolvedores e cliente, integrando entregas entre front-end, back-end e produto para manter o fluxo de desenvolvimento eficiente. | 
| **Adaptabilidade** | Me ajustei rapidamente às mudanças de escopo, novas demandas e diferentes tecnologias utilizadas no projeto, mantendo produtividade e qualidade nas entregas. | 
