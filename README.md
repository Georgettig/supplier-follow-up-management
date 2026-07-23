# 🧾 Supplier Follow-Up Management

> Aplicação desenvolvida em **Python** para automatizar o acompanhamento de pedidos de compras, identificar atrasos de entrega, controlar cobrança de fornecedores e fornecer indicadores gerenciais por meio de uma interface interativa construída com **Streamlit**.

## 📖 Sobre o projeto

Este projeto foi desenvolvido para solucionar um problema observado durante minha atuação no setor de Suprimentos de uma organização.

O acompanhamento dos pedidos de compra era realizado por meio de planilhas eletrônicas, exigindo consultas frequentes para identificar pedidos atrasados, fornecedores que deveriam ser cobrados e indicadores de desempenho da área.

Esse processo consumia muito tempo, era repetitivo e dificultava a visualização rápida da situação dos pedidos.

Para resolver esse problema, foi desenvolvida uma aplicação em **Python** e **Streamlit**, para automatizar toda a análise dos pedidos, permitindo consultas dinâmicas, aplicação de filtros e geração de indicadores em tempo real.

## 🏭 Contexto

Na rotina da área de suprimentos, centenas de pedidos de compra precisam ser acompanhados diariamente devido a sua criticidade de utilização nas áreas internas da organização.

Cada pedido possui:
- fornecedor;
- comprador responsável;
- data do pedido;
- data prevista de entrega;
- valor total;
- situação da cobrança (cobrado ou não).

O acompanhamento manual dessas informações dificulta a identificação de prioridades e aumenta o risco de atrasos no processo de compras.

Portanto, o sistema desenvolvido centraliza essas informações em uma única interface, permitindo que o usuário acompanhe rapidamente toda a sua carteira de pedidos.

## 🎯 Objetivos

- Automatizar o acompanhamento de pedidos de compra.
- Identificar automaticamente pedidos atrasados.
- Destacar fornecedores que necessitam de follow-up.
- Centralizar as informações em um dashboard interativo.
- Reduzir atividades manuais de acompanhamento.

## 🚀 Funcionalidades

✅ Importação automática da base de pedidos.

✅ Cálculo automático do status dos pedidos.

✅ Identificação de pedidos atrasados.

✅ Identificação de pedidos próximos ao vencimento.

✅ Controle de fornecedores já cobrados.

✅ Histórico de cobranças.

✅ Dashboard interativo.

✅ Filtros por fornecedor, comprador e número do pedido.

✅ Relação automática entre pedidos e fornecedores.

✅ Envio automático de e-mail para fornecedor.

✅ Atualização automática da base de pedidos cobrados.

## 🔄 Fluxo do processamento

```text
              Base de Pedidos (Excel)
                        │
                        ▼
               Leitura dos arquivos
                        │
                        ▼
          Tratamento e preparação dos dados
                        │
                        ▼
         Cálculo automático do Status
                        │
                        ▼
          Aplicação dos filtros
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
 Dashboard Interativo        Enviar Cobrança
                                      │
                                      ▼
                      Consulta à base de fornecedores
                                      │
                                      ▼
                   Relacionamento pelo código do fornecedor
                                      │
                                      ▼
                     Recuperação do e-mail correspondente
                                      │
                                      ▼
                   Integração com Outlook (versão original)
                                      │
                                      ▼
                   Atualização do histórico de cobranças
```

## 📧 Automação do Follow-Up

Além da análise dos pedidos, o sistema foi desenvolvido para automatizar o processo de cobrança de fornecedores.

Para isso, a aplicação utiliza uma base auxiliar contendo o cadastro dos fornecedores e seus respectivos endereços de e-mail.

Durante o processo de cobrança, o sistema realiza automaticamente:
- identificação dos pedidos selecionados pelo filtro;
- localização do fornecedores correspondente;
- relacionamento entre código do fornecedor na base de pedidos e no cadastro de fornecedores;
- seleção do endereço de e-mail com base no código do fornecedor;
- preparação das informações para envio da cobrança.

Na versão original do projeto, essa funcionalidade estava integrada ao **Microsoft Outlook**, permitindo o envio dos e-mails diretamente pela aplicação.

Porém, por questões de segurança e confidencialidade, a integração com o Outlook foi removida da versão publicada neste repositório, mantendo a estrutura responsável pela seleção e preparação dos dados.

## 🗂 Base de fornecedores

A aplicação utiliza uma base de dados auxiliar contendo o cadastro dos fornecedores.

Cada fornecedor possui um código único utilizado como chave para selecionar os pedidos da base principal com endereço de e-mail.

Essa estrutura permite automatizar o processo de cobrança sem necessidade de seleção manual dos destinatários.

| Campo | Finalidade |
|--------|------------|
| Código | Identificador único do fornecedor |
| Fornecedor | Nome do fornecedor |
| E-mail | Endereço utilizado para envio das cobranças |

## 📋 Regras de negócio

O sistema implementa automaticamente algumas regras utilizadas pelo setor de Suprimentos, como:

| Regra | Descrição |
|--------|-----------|
| Pedido atrasado | Data prevista de entrega menor ou igual à data atual. |
| Dentro do prazo | Data prevista de entrega maior que a data atual. |
| Cobrar fornecedor | Pedidos com entrega prevista para os próximos 30 dias e que ainda não foram cobrados. |
| Histórico de cobrança | Após registrar uma cobrança, o pedido passa automaticamente para o histórico de pedidos cobrados. |

## 📊 Indicadores disponíveis

O dashboard apresenta diversos indicadores para apoio à tomada de decisão.
- Quantidade de pedidos atrasados
- Quantidade de pedidos dentro do prazo
- Quantidade de pedidos cobrados
- Quantidade de pedidos pendentes de cobrança
- Ranking de compradores
- Ranking de fornecedores
- Consulta dinâmica através de filtros

## 📈 Visualizações

A aplicação gera automaticamente gráficos utilizando **Plotly**.
- Status do pedido
- Situação da cobrança
- Ranking de compradores
- Ranking de fornecedores

## 🏗 Arquitetura da aplicação

```text
                     Base Excel
                          │
                          ▼
                    database.py
                          │
                          ▼
                 Tratamento dos Dados
                          │
                          ▼
                      Home.py
                          │
           ┌──────────────┴──────────────┐
           ▼                             ▼
     Dashboard                        Filtros
           │                             │
           └──────────────┬──────────────┘
                          ▼
                Preparação das cobranças
                          │
                          ▼
          Base de fornecedores (E-mails)
                          │
                          ▼
               Outlook (versão original)
```

## 📂 Estrutura do projeto

```text
procurement-follow-up-dashboard/
│
├── dados/
│   ├── pedidos.xlsx                 # Base principal de pedidos
│   ├── fornecedores.xlsx            # Cadastro de fornecedores
│   └── pedidos_cobrados.xlsx        # Histórico das cobranças realizadas
│
├── pages/
│   └── Graficos.py                  # Dashboard com indicadores gráficos
│
├── database.py                      # Leitura e tratamento da base de dados
├── Home.py                          # Interface principal da aplicação
├── requirements.txt                 # Dependências do projeto
└── README.md                        # Documentação
```

## ⚙ Tecnologias utilizadas

### Linguagem:
- Python

### Interface:
- Streamlit

### Manipulação de Dados:
- Pandas

### Visualização:
- Plotly Express

### Fontes de Dados:
- Microsoft Excel

### Integração:
- Microsoft Outlook *(versão original do projeto)*

### Controle de Versão:
- Git
- GitHub

## 💡 Desafios do desenvolvimento

Durante o desenvolvimento alguns desafios precisaram ser solucionados.

- Conversão correta das datas.
- Tratamento de diferentes formatos de dados.
- Atualização automática do histórico de cobranças.
- Implementação de filtros dinâmicos.
- Integração entre base de dados e informações filtradas.
- Preparação automática dos e-mails para cobrança.
- Organização da aplicação em múltiplas páginas utilizando Streamlit.

## 📸 Demonstração

### Tela Principal:

<img width="1351" height="583" alt="image" src="https://github.com/user-attachments/assets/6b0c53cc-bdab-4c89-82fa-aaa420c169fd" />

### Seleção de Filtros e Envio de E-mails:

<img width="1299" height="465" alt="image" src="https://github.com/user-attachments/assets/f4500390-2706-40a3-a880-cc0764bdfb87" />

### Indicadores de Status/Situação do Pedido:

<img width="1060" height="422" alt="image" src="https://github.com/user-attachments/assets/312de508-ad49-4538-972b-6fa4ef762cd8" />

### Indicadores de Comprador/Fornecedor por Pedido:

<img width="991" height="397" alt="image" src="https://github.com/user-attachments/assets/d392bb70-89e6-4192-9e64-eee6b046f874" />

## 💻 Como executar

Clone o projeto

```bash
git clone https://github.com/Georgettig/supplier-follow-up-management.git
```

Crie um ambiente virtual

```bash
python -m venv .venv
```

Ative o ambiente

**Windows**

```bash
.venv\Scripts\activate
```

**Linux / macOS**

```bash
source .venv/bin/activate
```

Instale as dependências

```bash
pip install -r requirements.txt
```

Execute a aplicação

```bash
streamlit run Home.py
```

> **Observação:** A versão pública do projeto não possui a estrutura da funcionalidade de envio de e-mails, devido ao fato de a integração com o Microsoft Outlook ter sido removida para preservar credenciais e configurações do ambiente corporativo.

## 👨‍💻 Autor

**Guilherme Georgetti Albuquerque Galvão**

Analista de Dados / Engenheiro de Produção — UNESP

🔗 LinkedIn: *www.linkedin.com/in/guilherme-georgetti*
