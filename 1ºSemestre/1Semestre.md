
## 1° Semestre • 2022-1
### Mó Viagem
<p>Parceiro Acadêmico: <a href="https://fatecsjc-prd.azurewebsites.net/">Faculdade de Tecnologia de São José dos Campos</a></p>
<p align = "center"><img src= "imagens/logo_api_1.png" width="300" height="300"></p>
<p>A aplicação Mó Viagem é uma assistente virtual de viagens, que tem como objetivo auxiliar o planejamento de viagens futuras. O usuário pode pedir informações, pontos turísticos, curiosidades e deixar registrado quais os próximos destinos ele quer conhecer entre outras funcionalidades. É possível também perguntar a previsão do tempo para cada destino.</p>

## Tecnologias Utilizadas

* __Python:__ Linguagem de programação backend;
* __SpeechRecognition:__ Tecnologia que permite um dispositivo ou sistema reconhecer e interpretar a fala humana;
* __PyAudio:__ Biblioteca do Python que fornece uma interface para trabalhar com aúdio;
* __API OpenWeather:__ Interface de programação de aplicativos fornecida pela OpenWeather, que permite acesssar dados metereológicos em tempo real e previsões do tempo para qualquer lugar do mundo;
* __Pandas:__ Biblioteca do Python para análise e manipulação de dados;
* __Wikipédia:__ Biblioteca do Python que permite pesquisar e recuperar conteúdo da Wikipédia;
* __Requests:__ Biblioteca do Python para fazer requisições HTTP de forma simplificada;
* __Translator:__ Biblioteca que traduz textos para diferentes idiomas;
* __Holidays:__ Biblioteca que fornece informações sobre feriados em diversos países;
* __Re:__ Biblioteca do Python que permite pesquisar e manipular texto usando expressões regulares;
* __Webbrowser:__ Biblioteca do Python que permite abrir de maneira fácil URLs em navegadores da web padrão do sistema;
* __Pyttsx3__: Biblioteca do Python que fornece uma interface para síntese de voz.
<br><br>  

## Contribuições Pessoais 
### Transformação de texto para voz
<p>Para permitir a comunicação por voz com o usuário, a aplicação deve ser capaz de transformar texto em voz usando tecnologias específicas. Isso implica a integração de sistemas de síntese de voz que convertem o texto fornecido pela aplicação em uma saída de áudio natural e compreensível.
Essas tecnologias facilitam a interação entre o usuário e a aplicação, permitindo que o usuário ouça informações, respostas e instruções fornecidas pela aplicação de forma clara e concisa. Essa capacidade de comunicação por voz torna a interação com a aplicação mais intuitiva e acessível, além de oferecer uma experiência mais envolvente e dinâmica para o usuário.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p> Como a aplicação se trata de uma assistente virtual, se espera que a mesma se comunique com o usuário por meio de voz, para que o usuário tenha uma experiência lúdica e de fácil compreensão. Por meio da biblioteca Pyttsx3 do Python, é possível tranformar textos em voz. Sua lógica é bem simples, deve ser iniciado o mecanismo de síntese de voz, depois deve ser passado o texto que deve ser tranformado em voz e por fim o programa aguarda até que todo o texto tenha sido falado antes de prossegir.</p>
  <p>Abaixo é mostrado uma aplicação simples de como funciona a tranformação de texto para voz:</p>
  
  ```python
  def convertFala(texto):
  engine = pyttsx3.init()
  engine.say(texto)
  engine.runAndWait()
  ```
</details>
<br>

### Lista de Desejos
<p>Esta funcionalidade permite que o usuário armazene informações sobre locais que deseja visitar, incluindo o nome do município, estado e seus principais pontos turísticos. Essas informações são salvas em um arquivo .txt, possibilitando que o usuário acesse sua lista de desejos e planeje um roteiro personalizado com base em suas preferências registradas.</p>
<details>
<summary><h4>Mais detalhes</h4></summary>
  <p>A lista de desejos é feita por meio da criação de um arquivo .txt, sendo que a própria aplicação cria e atualiza este arquivo. Após a criação do mesmo, a aplicação pede algumas informações sobre o local que ele deseja visitar. O usuário fala as informações, a aplicação converte a fala em texto e armazena as informações dentro do arquivo. De um ponto de vista mais técnico, é necessário que a aplicação crie um arquivo .txt, em seguida a aplicação pergunta ao usuário que ação ele deseja realizar na lista de desejos, visualizar a lista de desejos ou adicionar um novo destino. Caso o usuário opte por visualizar a lista desejos, a aplicação lê o arquivo .txt e mostra na tela as informações dos destinos, além de responder por voz também. Se o usuário optar por adicionar um novo destino, a aplicação irá dizer para o usuário falar sobre o local desejado, em seguida a aplicação abre a edição do arquivo .txt e armazena as informações que foram ditas pelo o usuário. Para deletar ou editar alguma informação da lista de desejos, é necessário que o usuário abra o arquivo e realize as ações que deseja executar.</p>
  <p>Abaixo é mostrado como a lista de desejos é realizada na aplicação:</p>
  
  ```python
    elif "desejo" in texto:
            convertFala("Você deseja visualizar a lista ou adicionar")
            print("\n")
            print("1- Visualizar")
            print("2- Adicionar")
            print("\n")

            rec = sr.Recognizer()

            with sr.Microphone() as mic:
                print("Escolha uma opção: ")
                rec.adjust_for_ambient_noise(mic)
                audio = rec.listen(mic)

            resposta = rec.recognize_google(audio, language="pt-BR")

            if ("visualizar" in resposta):
                arquivo = open('lista.txt', 'r')
                print("----Lista de Desejos----")

                for linha in arquivo:
                    print(linha.rstrip())
                    convertFala(linha.rstrip())

                print("Para retirar um destino da lista, vá até o arquivo lista.txt e elimine o que desejar")
                convertFala("Para retirar ou alterar um destino da lista, vá até o arquivo lista.txt e elimine ou altere o que desejar")
                arquivo.close()

            elif ("adicionar" in resposta):
                from classe import listadesejo
                arquivos.append(listadesejo())
                arquivo = open('lista.txt', 'a')

                convertFala("Qual cidade você deseja visitar")
                rec = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Qual o nome da cidade: ")
                    rec.adjust_for_ambient_noise(mic)
                    audio = rec.listen(mic)

                nomecidade = rec.recognize_google(audio, language="pt-BR")

                arquivos[contador].setnomecidade(nomecidade)

                convertFala("Qual o nome do estado brasileiro")
                rec2 = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Qual o nome do estado: ")
                    rec2.adjust_for_ambient_noise(mic)
                    audio = rec2.listen(mic)

                estado = rec2.recognize_google(audio, language="pt-BR")

                arquivos[contador].setestado(estado)

                convertFala("Quais são os pontos turísticos")
                rec3 = sr.Recognizer()

                with sr.Microphone() as mic:
                    print("Quais os pontos turísticos: ")
                    rec3.adjust_for_ambient_noise(mic)
                    audio = rec3.listen(mic)

                ponto = rec3.recognize_google(audio, language="pt-BR")

                arquivos[contador].setponto(ponto)

                arquivo.write("--------------------" + "\n")
                arquivo.write("Nome da Cidade:" + arquivos[contador].getnomecidade() + "\n")
                arquivo.write("Nome do Estado:" + arquivos[contador].getestado() + "\n")
                arquivo.write("Pontos Turísticos:" + arquivos[contador].getponto() + "\n")
                arquivo.write("--------------------" + "\n")
                arquivo.close()

                print("Destino adicionado com sucesso")
                convertFala("Destino adicionado com sucesso")
            else:
                convertFala("Não entendi, poderia repetir")
  ```
</details>
<br>
<hr></hr>
<br><br>

## Aprendizados
<p>Durante o projeto da API do 1ºSemestre atuei como desenvolvedor, elaborando e construindo implementações do projeto. Pude aumentar o meu conhecimento na linguagem Python e utilizá-la para diferentes propósitos. Além de compreender como funciona a lógica de programação, conceitos de repetição, conceitos de condicionais entre outros paradigmas da programação.</p>

## � Soft Skills  

## 1. **Comunicação Clara**  
   - **Descrição**  
     Trabalhar em equipe exige transmitir ideias de forma eficiente, evitando ruídos e retrabalho.

     Durante um projeto de implementação de um novo sistema, atuei como ponte entre desenvolvedores e o setor comercial, traduzindo termos técnicos para uma linguagem acessível. Isso garantiu alinhamento rápido e reduziu erros nos requisitos em **30%**.  

## 2. **Resolução de Problemas**  
   - **Descrição**  
     Imprevistos podem paralisar operações se não forem resolvidos com agilidade e criatividade.

     Identifiquei um gargalo no fluxo de entregas usando análise de dados e propus um redesenho das rotas, reduzindo o tempo de entrega em **15%**.  

## 3. **Adaptabilidade**  
   - **Descrição**  
     Mudanças de escopo ou prioridades são comuns em ambientes dinâmicos.

     Quando um cliente alterou urgentemente as especificações de um produto, reestruturei minha agenda e priorizei as novas demandas sem impactar o prazo final.  

---  

### 💻 Hard Skills  

## 1. **Python (Análise de Dados)**  
   - **Descrição**  
     Automatizar processos manuais aumenta a eficiência e reduz falhas humanas.

     Desenvolvi um script em Python para consolidar relatórios mensais de vendas, que antes levavam **8 horas manuais**. A solução passou a gerar os dados em **20 minutos**.  

## 2. **Gestão de Projetos (Metodologia Ágil)**  
   - **Descrição**  
     Equipes multidisciplinares precisam de coordenação clara para entregas iterativas.

     Como Scrum Master em um projeto de TI, organizei *sprints* quinzenais e *daily meetings*, resultando em uma entrega **10% mais rápida** que o planejado.  

## 3. **Pacote Office Avançado (Excel, Power BI)**  
   - **Descrição**  
     Tomadas de decisão precisam ser baseadas em dados visualizados de forma intuitiva.
       
     Criei um dashboard no Power BI para monitorar KPIs de logística, permitindo que a equipe identificasse tendências e ajustasse estratégias em **tempo real**.  

<hr></hr>
<br>

