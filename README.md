<h1 align="center">Olá, eu sou o Neres 👋</h1>

<p align="center">
  <b>Automação de processos com Python · Engenharia de Software na FIAP</b><br/>
  Aprendiz na área de Manutenção do GPA (Grupo Pão de Açúcar)
</p>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=2E75B6&center=true&vCenter=true&width=520&lines=Python+%2B+Playwright+%2B+SAP+GUI;Processo+manual+%E2%86%92+automa%C3%A7%C3%A3o;Automatize+o+que+%C3%A9+repetitivo" alt="Typing SVG" />
</p>

---

## 👨‍💻 Sobre mim

Trabalho no back-office da Manutenção do GPA: contas a pagar, notas fiscais de serviço (NFS-e), pedidos de compra no **Coupa**, ocorrências no **SAP** e chamados no **ServiceNow**, com contato direto com fornecedores.

Boa parte dessa rotina é repetitiva. Quando identifico uma tarefa que a equipe faz na mão, item por item, eu transformo em uma automação em Python. Hoje várias delas rodam no dia a dia da área.

- 🎓 Engenharia de Software na **FIAP** (2º ano · formatura em dez/2028)
- 🌎 Inglês avançado
- 🔎 Aberto a oportunidades de **estágio em desenvolvimento, automação ou dados**

---

## ⚙️ Como eu construo uma automação

1. **Mapeio o processo manual** direto na tela: cada clique, campo e botão do sistema
2. **Uso a planilha que a equipe já trabalha como entrada**, sem obrigar ninguém a mudar o formato
3. **Automatizo com Python**: Playwright para sistemas web e SAP GUI Scripting para o SAP
4. **Valido cada etapa**: a automação confere se a ação deu certo antes de seguir para o próximo item e separa o que falhou para reprocessar
5. **Não guardo senha no código**: o login é feito uma vez à mão num perfil de navegador salvo, e os dados do ambiente ficam em `.env`
6. **Deixo rastro de tudo**: relatório de cada execução com o que deu certo, o que falhou e por quê, mais print da tela no erro
7. **Meço o tempo** da automação contra o processo manual
8. **Uso IA (Claude)** como apoio para modelar a lógica, escrever e revisar o código

---

## 🤖 Automações (RPA)

### 📥 Download de notas fiscais
Baixa em lote os PDFs das notas fiscais que a área precisa arquivar todo mês, a partir da planilha de ocorrências.

- Lê a planilha e encontra sozinha as colunas de nota e ocorrência pelo nome do cabeçalho (e pede confirmação antes de começar)
- **No SAP**, consulta cada ocorrência via SAP GUI Scripting e captura o PDF gerado em segundo plano, sem depender de cliques na tela
- O que não existe no SAP é buscado **no portal web** do sistema de notas com Playwright; antes de baixar, confere se o resultado na tela é mesmo a ocorrência buscada, para não salvar a nota errada
- Confere se cada arquivo é um PDF de verdade, compara a pasta com a planilha e reprocessa só o que faltou
- Gera relatório em Excel colorido por status e mostra progresso com estimativa de término

**Resultado:** tarefa de ~6 dias/mês dividida entre 2 pessoas passou a ser feita por 1, na metade do tempo.
`Python` `SAP GUI Scripting (win32com)` `Playwright` `openpyxl`

### 🧾 Geração de pedidos no Coupa
Lança requisições de compra no Coupa a partir da nota do fornecedor ou de uma planilha, uma requisição atrás da outra.

- Lê a nota em vários formatos: **XML da NF-e**, texto ou PDF da DANFE (com regex) e até **PDF escaneado ou foto**, usando o OCR do próprio Windows
- Distribui frete, ST e IPI entre os itens para as linhas fecharem exatamente no valor total da nota
- Escolhe o código de item de cada linha por histórico, regras e semelhança de descrição, e verifica no Coupa se o item pode ser usado
- **Aprende com o uso**: guarda os códigos aprovados e reprovados na própria planilha para as próximas execuções
- Preenche cabeçalho, fornecedor, valores, centro de custo e conta; no fim, confere as linhas lançadas contra a nota
- Dá para pausar, parar com segurança e continuar depois de onde parou

**Resultado:** 3x mais rápido que o lançamento manual, com perfil pronto também para o fluxo de outra colega da equipe.
`Python` `Playwright` `XML` `Regex` `OCR` `openpyxl`

### 🎫 [Fechamento de chamados no ServiceNow](https://github.com/Neres73/automacao_servicenow_chamados)
Encerra em lote as ordens de serviço já atendidas, a partir da planilha preenchida com os dados do atendimento.

- Para cada chamado, localiza a tarefa, **confere se o técnico atribuído é o mesmo da planilha** e segue o fluxo de status até o encerramento
- Preenche horários reais de início e fim, código de fechamento e quem validou
- Confirma que cada mudança de status foi aceita pelo sistema antes de seguir (e tenta de novo se não foi)
- Grava o status de volta na planilha e gera relatório CSV com a lista de falhas

**Resultado:** processo que era dividido pela equipe hoje é feito por 1 pessoa.
`Python` `Playwright` `openpyxl`

### Outras automações no Coupa

| Automação | O que faz |
|-----------|-----------|
| ✅ **[Aprovações](https://github.com/Neres73/Coupa_aprovacoes)** | Aprova requisições abaixo de R$ 10 mil |
| 📦 **[Recebimento](https://github.com/Neres73/Coupa_recebimento)** | Faz o recebimento das requisições listadas na planilha |
| 🔁 **Troca de fornecedor** | Percorre todas as linhas da requisição (inclusive em várias páginas), troca o fornecedor indefinido pelo CNPJ correto e submete para aprovação |
| ❌ **Cancelamento de pedidos** | Abre cada pedido e solicita o cancelamento |
| 📄 **PDF de pedidos** | Baixa o PDF de cada pedido e salva com o número do pedido |

`Python` `Playwright` `openpyxl`

> Repositórios sem link são de uso interno e não estão públicos.

---

## 📊 Dados & Análise

| Projeto | O que faz | Tech |
|---------|-----------|------|
| 📈 **Dashboard da fila de pagamentos** | Meu primeiro BI: acompanha as notas pendentes de pagamento da Manutenção com KPIs de valor e quantidade, aging, top fornecedores e status. Antes, a fila era acompanhada só em planilha | Power BI, Power Query |
| 🔍 **Cruzamento de contrato com estoque de fornecedor** | Compara 3.277 itens de contrato com 697 descrições do estoque de um fornecedor. As descrições não batem palavra por palavra (abreviações, texto cortado), então usei fuzzy matching com regras de confiança por categoria e saída colorida por faixa de certeza | Python, RapidFuzz, openpyxl |

---

## 🎓 Projetos acadêmicos (FIAP)

| Projeto | Descrição | Tech |
|---------|-----------|------|
| 📡 **[Bateia](https://github.com/RafaellSantiagoMS/bateia-app)** | Plataforma de inteligência conversacional para o time comercial da TOTVS: transcrições de reuniões viram resumo, sinais de churn/up-sell e Índice de Trusted Advisor — GS FIAP 2026, em grupo | React, Vite |
| 📉 **Regressão Linear + Streamlit** | Compara modelos de regressão (baseline, simples, múltipla e polinomial) por MAE, RMSE e R², com app interativo — em grupo | Python, Pandas, Streamlit |
| 🧮 **[Dynamic Programming](https://github.com/Neres73/Dynamic-programming)** | Estação terrestre que recebe e processa alertas de queimadas, enchentes e deslizamentos captados por satélites — GS FIAP 2026 | Python |
| ⚽ **[PassaBola](https://github.com/PedroMarchese01/Passa-Bola)** | Sistema web de gerenciamento de eventos esportivos com dashboard, CRUD e geração de chaves — GS FIAP 2025, em grupo | React, Tailwind, Chart.js |
| 🛰️ **SmartInfra Orbital** | Sistema de monitoramento de infraestrutura espacial (console app) | Java, DDD |
| 🏠 **[Airbnb Clone](https://github.com/Neres73/CP-CAIO)** | Landing page responsiva simulando um anúncio do Airbnb — Flexbox, Grid, galeria e avaliações | HTML5, CSS3 |

---

## 🛠️ O que eu sei

**Uso no dia a dia (trabalho):**

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Playwright-45ba4b?style=for-the-badge&logo=playwright&logoColor=white"/>
  <img src="https://img.shields.io/badge/SAP_GUI_Scripting-0FAAFF?style=for-the-badge&logo=sap&logoColor=white"/>
  <img src="https://img.shields.io/badge/Excel_|_openpyxl-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white"/>
  <img src="https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black"/>
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white"/>
</p>

Nas automações também uso: expressões regulares, leitura de XML, OCR local, `win32com`/`pywinauto` para janelas do Windows, variáveis de ambiente (`.env`), logs e relatórios em Excel/CSV.

**Uso em projetos da faculdade:**

<p>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white"/>
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB"/>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white"/>
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white"/>
  <img src="https://img.shields.io/badge/Oracle_SQL-F80000?style=for-the-badge&logo=oracle&logoColor=white"/>
</p>

**Estudando agora:**

<p>
  <img src="https://img.shields.io/badge/Java_Back--End-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scrum-6DB33F?style=for-the-badge&logo=scrumalliance&logoColor=white"/>
</p>

---

## 📊 GitHub Stats

<p align="center">
  <img height="160" src="https://github-readme-stats.vercel.app/api?username=Neres73&show_icons=true&theme=tokyonight&hide_border=true"/>
  <img height="160" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Neres73&layout=compact&theme=tokyonight&hide_border=true"/>
</p>

---

## 📫 Contato

<p>
  <a href="https://www.linkedin.com/in/gustavo-neres-dos-santos-699046355/">
    <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
  <a href="mailto:gustavo.neres763@gmail.com">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>
</p>

---

<p align="center">
  <i>"Automatize o que é repetitivo. Foque no que importa."</i>
</p>
