<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Análise de Performance e Estudo de Detecção de Anomalias em Máquinas de Ar Condicionado

#### Aluno: [Lucas Amaral Lassance Cabral](https://github.com/lassancetecnologia/tcc_bimaster_2019.4)
#### Orientador: [Leonardo Mendoza]

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/lassancetecnologia/tcc_bimaster_2019.4/blob/main/TCC_BI_MASTER_LUCAS_LASSANCE_2019_4_REV02.ipynb). <!-- caso não aplicável, remover esta linha -->





---

### Resumo

O presente trabalho se destina à análise de performance e estudo para detecção de anomalias em dados coletados de máquinas de ar condicionado do tipo inverter/compressor. A partir de gateway de comunicação ligado à máquina, foi possível adquirir dados reais de diversas grandezas a serem estudadas por três meses. Este estudo tem por objetivo avaliar possibilidades de detecção de anomalias a serem implantadas em sistemas embarcados.

Máquinas de ar condicionado são muitas vezes itens críticos às operações prediais e industriais e representam no geral, a maior contribuição de consumo de energia dos empreendimentos, além de dispensarem grandes recursos de manutenção e operação, então, usar métodos inteligentes para apontar o melhor uso dos equipamentos aumentando sua performance e vida útil, planejar melhor atividades de manutenção e evitar paradas não planejadas é de grande interesse aos gestores.

A performance da máquina foi estudada através de sua capacidade de manter a temperatura controlada dentro de certos limites definidos.

Foram utilizados métodos puramente estatísticos e algoritmos de machine learning para identificar anomalias presentes nos dados e avaliar os resultados para novas amostras simuladas com anomalias bem definidas. Iniciando por análises de z-core e z-score modificado, passando por método de clusterização DBSCAN e concluindo com metodologia de treinamento supervisionado foi possível realizar testes abrangentes e determinar as melhores soluções para o problema de identificação de anomalias. 

### Abstract

The present work is intended for performance analysis and study to detect anomalies in data collected from inverter/compressor type air conditioning machines. From a communication gateway connected to the machine, it was possible to acquire real data of several magnitudes to be studied for three months. This study aims to evaluate possibilities for detecting anomalies to be implemented in embedded systems.

Air conditioning machines are often critical items for building and industrial operations and represent, in general, the largest contribution of energy consumption of projects, in addition to not requiring large maintenance and operation resources, so use intelligent methods to point out the best use of the equipment increasing its performance and useful life, better planning maintenance activities and avoiding unplanned stoppages is of great interest to managers.

The machine's performance was studied through its ability to keep the temperature controlled within certain defined limits.

Purely statistical methods and machine learning algorithms were used to identify anomalies present in the data and evaluate the results for new simulated samples with well-defined anomalies. Starting with z-core and modified z-score analysis, going through the DBSCAN clustering method and ending with supervised training method, it was possible to perform extensive tests and determine the best solutions for the problem of identifying anomalies.



### 1. Introdução

Máquinas de ar condicionado são grandes aliadas ao conforto dos brasileiros, porém, são responsáveis por grande parte do consumo de energia elétrica de empreendimentos como edifícios comerciais, shopping centers, hospitais e tantos outros. A coleta e análise de dados provenientes das máquinas e ambientes pode ser extremamente útil na redução da energia consumida, além otimizar processos de manutenção, otimizando recursos e aumentando a vida útil destes equipamentos, que normalmente possuem alto valor de venda e/ou reposição, sem mencionar em impactos ao funcionamento de empresas e estabelecimentos de todos os tipos.

Uma máquina do tipo Inverter, que utiliza uma substância refrigerante para resfriar o ar a ser reinserido no ambiente, foi monitorada por três meses através de gateway próprio do fabricante, fornecendo dados em protocolo aberto Modbus RTU, possibilitando a leitura de seus dados, estruturação das informações e envio de pacotes periódicos para um ambiente em nuvem, onde os dados foram armazenados e posteriormente lidos para análise.

Os dados e resultados obtidos por este estudo foram consolidados em documento Google Docs (disonível no código fonte) para que, em uma extensão deste trabalho, estes resultados sejam aplicados para novas amostras de dados e apresentados ao cliente em forma de relatório.


### 2. Tratamento de Dados

Cada variável coletada do equipamento foi registrada disponibilizada através de chamadas GET (HTTP) que resultaram em arquivos csv indepentendes. Os seguintes passos foram realizados para a organização e tratamento dos dados para o início das análises:

- Chamada GET de todas as variáveis e armazenamento dos arquivos csv em Google Drive
- Leitura de cada um dos arquivos, retirando atributos de configuração e desnecessários
- União dos dados através da referência de tempo de cada uma das amostras
- Correção de fuso horário das amostras e exclusão de dados coletados com a máquina desligada


### 3. Análise de Performance

Existem várias formas para análise de performance de máquinas de ar condicionado, que dependem da real intenção ou necessidade do estudo. Neste caso, foi avaliada a capacidade do equipamento de manter-se razoavelmente próximo à temperatura desejada (setpoint) e programada na interface disponível ao longo do tempo.

- Para cada amostra foi calculado o erro de temperatura, dado pela temperatura do ambiente controlado subtraído do setpoint de temperatura
- Dadas tolerâncias de temperatura abaixo e acima do setpoint, foram calculados em horas os períodos em que a máquina ficou fora dos limites definidos pelas tolerâncias ao redor do setpoint
- A eficiência foi determinada pela porcentagem de tempo em que a máquina se manteve dentro dos limites


### 4. Estudos Estatísticos

Para o início de estudo de dados anômalos, primeiramente foram gerados gráficos de distribuição e de amostras ao longo do tempo para avaliação visual dos registros, assim como um gráfico de correlação entre as variáveis coletadas.

Abaixo, são relacionadas as variáveis disponibilizadas pela máquina:
- 'time', 'codigo_falha', 'controle_on_off_ihm', 'corrente_comp1', 'rpm_condensador', 'temp_amb_retorno', 'setpoint_temp_ihm', 'temp_descarga_comp1', 'temp_meio_condensador', 'temp_descarga_comp2', 'temp_dissipador_calor', 'frequencia_compressor', 'corrente_comp2', 'modo_ihm', 'temp_succao', 'tensao_barramentoinv', 'corrente_compressor', 'temp_externa', 'potencia'

Os códigos de falha, apesar de relevantes para a máquina, não se mostraram interessantes para a identificação de anomalias nas variáveis coletadas, por isso, foi descartada das análises. Foi notado que este indicador representa a parte eletrônica da máquina, que não é objeto deste estudo.

Em seguida, foram realizados cálculos estatísticos através de zcore e zscore modificado para identificação de dados discrepantes na base, que após testes, foi verificado o threshold adequado de 4. Os cálculos para anomalias negativas foram descartadas pois o objetivo é buscar altas temperaturas, correntes e frequências da máquina.
Com a introdução manual de anomalias na base, o threshold escolhido se manteve adequado em detectar amostras anômalas.


### 5. Detecção por Clusterização

Após testes de detecção de dados anômalos com os algoritmos k-means e DBSCAN, foi adotada a segunda opção por apresentar maior facilidade em separar dados com registros de valor razoavelmente alto.

A princípio, o uso do método DBSCAN não foi adequado pelo fato das variáveis apresentarem ordens de grandeza diferentes, por exemplo, temperaturas entre 10 e 30°C e valores de potência na casa de 50.000VA. Pelo fato do algoritmo usar densidade de pontos para determinar vizinhanças, foi necessária a normalização dos dados para que todos os atributos estivessem na mesma ordem e resultado fosse efetivo.


### 6. Detecção por Aprendizado Supervisionado

Para testes de classificação por método de aprendizado supervisionado foram geradas amostras sintéticas de registros com anomalias e utilizado o método KNN de classificação, apresentando excelente resultado.


### 7. Resultados

Com objetivo de realizar a detecção de anomalias foram realizados diversos testes, por vários métodos. 
O primeiro foi a análise puramente estatística, envolvendo zcore e zscore modificado, com bons resultados para threshold de 4.
Em seguida, foi utilizado método de clusterização DBSCAN, com muito bons resultados na separação de amostras de dados anômalos dos normais, se revelando também uma opção viável para resolução do problema.
Ainda nos métodos de aprendizado não supervisionado, foi testado o algoritmo Isolation Forest, que não se mostrou eficaz, provavelmente devido à correlação dos dados.
Por fim, foi utilizado um algoritmo de aprendizado supervisionado após a geração de dados sintéticos para balanceamento das classes de dados normais e anômalos, apresentando acurácia de 99,99%.


### 8. Conclusões

Concluí-se portanto que o problema de detecção de anomalias para máquinas de ar condicionado com coleta de variáveis similares às mencionadas neste trabalho pode ser solucionado através de diversas possibilidades de algoritmos e metodologias. 
A solução que se mostrou mais viável e eficiente foi a geração de dados sintéticos de classe anômala e uso de simples algoritmo de aprendizado supervisionado.

---

Matrícula: 192.110.210

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
