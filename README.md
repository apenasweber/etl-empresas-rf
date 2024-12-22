### **Projeto de ETL para Extração e Classificação de Empresas Brasileiras (Trust Works)**

#### **Objetivo do Projeto:**

Desenvolver um pipeline de ETL (Extração, Transformação e Carga) em Python para coletar, processar e categorizar dados de empresas do Brasil, extraídos diretamente do site da Receita Federal. A base resultante será pública, gratuita e servirá para mapear setores econômicos e identificar empresas que aparecem nas reclamações da Trust Works.

----------
## 📹 Assista ao Vídeo do Projeto  
[🔗 Assista ao vídeo no YouTube](https://youtu.be/5UPE6GonLOA)  

### **Escopo do Projeto:**

**1. Extração Automatizada de Dados (Receita Federal):**  
O projeto começa com a migração de um script já existente em **R** (videoaula: [YouTube](https://www.youtube.com/watch?v=MHGW706b-Zo&t=620s)) para **Python**. A automação deve permitir o download de arquivos de todos os estados do Brasil, sem a necessidade de alterar manualmente o parâmetro de UF (Unidade Federativa).

🔹 **Requisitos:**

-   O script deve realizar a extração automaticamente de todos os estados de uma vez.
-   Os arquivos serão baixados em uma pasta com o nome da data do download (formato: `AAAA-MM-DD`), facilitando a identificação da base mensal.

🔹 **Referência para Layout de Dados:**

-   Layout oficial: [Receita Federal - Layout de Dados Abertos CNPJ](https://arquivos.receitafederal.gov.br/cnpj/LAYOUT_DADOS_ABERTOS_CNPJ.pdf).

🔹 **Tecnologias Sugeridas:**

-   **Python (Async e PySpark)** para maior eficiência no processamento de grandes volumes de dados (~43GB).

----------

### **2. Transformação e Limpeza de Dados:**

Após a extração, o pipeline deve realizar a limpeza dos dados, removendo duplicatas e corrigindo inconsistências.

**🔸 Classificação das Empresas por Setor (CNAE-FISCAL):**

-   **Campo Principal:** **CNAE-FISCAL** (Localizado no Campo 376 do layout).
-   **Descrição:** Indica a atividade econômica principal da empresa.
-   **Processo:**
    1.  **Mapeamento por Dicionário de Setores:**  
        Crie um dicionário Python para mapear os primeiros dois dígitos do CNAE-FISCAL para um setor. 

**cnae_to_sector = { 
'47': 'Comércio Varejista', 
'62': 'Tecnologia da Informação', 
'01': 'Agricultura', 
'23': 'Construção Civil', } 
df['Setor'] = df['CNAE-FISCAL'].str[:2].map(cnae_to_sector)**

      
   
   2.  **CNAE Secundário (Campo 18):**  
        Se o CNAE principal não for suficiente para definir o setor, verifique as atividades secundárias.

----------

### **3. Carga e Organização dos Dados:**

Os dados transformados serão salvos em arquivos CSV organizados por setor, facilitando a consulta.

🔹 **Categorias de Setores:**

1.  Agências de Atendimento e Recrutamento
2.  Arte e Entretenimento
3.  Casa e Construção
4.  Educação
5.  Moda
6.  PET
7.  Serviços Essenciais
8.  Softwares
9.  Transportes e Serviços
10.  Veículos e Acessórios
11.  Alimentos e Bebidas
12.  Bancos e Financeiras
13.  Conteúdo Sensível
14.  Eletroeletrônicos
15.  Mãe e Bebê
16.  Saúde
17.  Setor Imobiliário
18.  Supermercados e Atacados
19.  Turismo e Lazer
20.  Apostas
21.  Beleza e Estética
22.  Editoriais, Conteúdo e Informação
23.  Fidelidade - Pontos
24.  Móveis e Decoração
25.  Seguradoras
26.  Sindicatos, Associações e ONGs
27.  Telefonia, TV e Internet
28.  Varejo

🔹 **Exemplo de Saída:**
`bancos.csv` 

----------

### **Métricas e Indicadores de Sucesso:**

1.  **Extração:**

-   O script realiza o download completo da base da Receita Federal sem falhas ou necessidade de intervenção manual.
-   A pasta com o nome da data contém todos os arquivos de estados em CSV.

2.  **Transformação:**

-   Duplicatas e inconsistências são removidas.
- O "#" é removido do inicio de cada célula
-   Empresas corretamente classificadas de acordo com o CNAE-FISCAL.

3.  **Carga:**
- Os arquivos finais são facilmente entendíveis, sem IDs de informações que poderiam estar como texto(com exceção dos cnaes).
-   Dados são organizados em arquivos CSV por setor, prontos para serem indexados e utilizados pela Trust Works.

----------

### **Benefícios do Projeto:**

-   **Transparência:** A base de empresas estará disponível gratuitamente para consulta pública.
-   **Prevenção de Fraudes:** Empresas fantasmas ou reincidentes podem ser identificadas, ajudando na detecção de fraudes trabalhistas.
-   **Eficiência:** A automatização economiza tempo e reduz erros humanos.
-   **Insights para Empresas:** A Trust Works poderá cruzar dados de reclamações com informações empresariais, gerando relatórios mais completos e detalhados.

Esse projeto impulsionará a Trust Works na construção de um banco de dados robusto, fortalecendo sua proposta de valor e expandindo seu impacto no mercado de trabalho brasileiro. 🚀
