<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Análise de Performance e Estudo de Detecção de Anomalias em Máquinas de Ar Condicionado

#### Aluno: [Lucas Amaral Lassance Cabral](https://github.com/link_do_github)
#### Orientador: [Leonardo Mendoza](https://github.com/link_do_github)

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/link_do_repositorio). <!-- caso não aplicável, remover esta linha -->

- [Link para a monografia](https://link_da_monografia.com). <!-- caso não aplicável, remover esta linha -->



---

### Resumo

O presente trabalho se destina à análise de performance e estudo para detecção de anomalias em dados coletados de máquinas de ar condicionado do tipo inverter/compressor. A partir de gateway de comunicação ligado à máquina, foi possível adquirir dados reais de diversas grandezas a serem estudadas por três meses. Este estudo tem por objetivo avaliar possibilidades de detecção de anomalias a serem implantadas em sistemas embarcados.

Máquinas de ar condicionado são muitas vezes itens críticos às operações prediais e industriais e representam no geral, a maior contribuição de consumo de energia dos empreendimentos, além de dispensarem grandes recursos de manutenção e operação, então, usar métodos inteligentes para apontar o melhor uso dos equipamentos aumentando sua performance e vida útil, planejar melhor atividades de manutenção e evitar paradas não planejadas é de grande interesse aos gestores.

A performance da máquina foi estudada através de sua capacidade de manter a temperatura controlada dentro de certos limites definidos.

Foram utilizados métodos puramente estatísticos e algoritmos de machine learning para identificar anomalias presentes nos dados e avaliar os resultados para novas amostras simuladas com anomalias bem definidas. Iniciando por análises de z-core e z-score modificado, passando por método de clusterização DBSCAN e concluindo com Isolation Forest foi possível realizar testes abrangentes e determinar as melhores soluções para o problema de identificação de anomalias. 

### Abstract

The present work is intended for performance analysis and study to detect anomalies in data collected from inverter/compressor type air conditioning machines. From a communication gateway connected to the machine, it was possible to acquire real data of several magnitudes to be studied for three months. This study aims to evaluate possibilities for detecting anomalies to be implemented in embedded systems.

Air conditioning machines are often critical items for building and industrial operations and represent, in general, the largest contribution of energy consumption of projects, in addition to not requiring large maintenance and operation resources, so use intelligent methods to point out the best use of the equipment increasing its performance and useful life, better planning maintenance activities and avoiding unplanned stoppages is of great interest to managers.

The machine's performance was studied through its ability to keep the temperature controlled within certain defined limits.

Purely statistical methods and machine learning algorithms were used to identify anomalies present in the data and evaluate the results for new simulated samples with well-defined anomalies. Starting with z-core and modified z-score analysis, going through the DBSCAN clustering method and ending with Isolation Forest, it was possible to perform extensive tests and determine the best solutions for the problem of identifying anomalies.



### 1. Introdução

Máquinas de ar condicionado são grandes aliadas ao conforto dos brasileiros, porém, são responsáveis por grande parte do consumo de energia elétrica de empreendimentos como edifícios comerciais, shopping centers, hospitais e tantos outros. A coleta e análise de dados provenientes das máquinas e ambientes pode ser extremamente útil na redução da energia consumida, além otimizar processos de manutenção, otimizando recursos e aumentando a vida útil destes equipamentos, que normalmente possuem alto valor de venda e/ou reposição, sem mencionar em impactos ao funcionamento de empresas e estabelecimentos de todos os tipos.

Uma máquina do tipo Inverter, que utiliza uma substância refrigerante para resfriar o ar a ser reinserido no ambiente, foi monitorada por três meses através de gateway próprio do fabricante, fornecendo dados em protocolo aberto Modbus RTU, possibilitando a leitura de seus dados, estruturação das informações e envio de pacotes periódicos para um ambiente em nuvem, onde os dados foram armazenados e posteriormente lidos para análise.


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


### 4. Modelagem

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

### 5. Modelagem

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

### 6. Resultados

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

### 7. Conclusões

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

---

Matrícula: 192.110.210

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
