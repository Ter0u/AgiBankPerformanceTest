**PROPOSTA**
Desenvolvimento de Script do Jmeter para execução de teste de performance dentro dos critérios de aceite propostos no desafio técnico do AgileBank


📝**CONSIDERAÇÕES SOBRE EXECUÇÃO:**
Tendo em vista o objetivo e critério de aceite de 250 requisições por segundo com aprovação percentil 90th inferior a 2 segundos
Desenvolvi um script de rampa no jmeter utilizando o UltimateThreadGroup no qual simula que 250 usuários simultâneos realizam requisições intermitentes, com ramp-up gradual até atingir o pico de 250 usuários, assim permitindo-nos avaliar o comportamento do microsserviço sob carga máxima planejada.

Além disso utilizei o relatório agregado e também gerei um report html onde ambos divergem em questão dos tempos de resposta pois o relatório agregado inclui o tempo de resposta de todas requests enquanto o de html pode acabar considerando somente as requisições com sucesso.
Contudo ambos relatórios são úteis para avaliar diferentes métricas onde no relatório html podemos ver o consolidados de requisições que falharam X que deram sucesso enquanto no relatório agregado temos uma avaliação do tempo de resposta mais preciso.


📊 **RESULTADOS:**
(Relatório com gráfico contendo execuções está junto ao projeto)
  🚀 POSITIVO - Com base em minhas execuções e relatório anexado junto ao jmx, o microsserviço atendeu ao critério de aceite de 90th inferior a 2 segundos.
  🚧 NEGATIVO - Contudo considerando outras métricas como o percentil 95th, nossa aplicação não está aderente aos critérios de aceite. 
Oque poderia ser fator ou débito técnico para investigação e buscar uma melhora em nossos serviços para encurtar o tempo médio de resposta.


**COMO CONFIGURAR E EXECUTAR SCRIPT DE PERFORMANCE:**
✅ PASSO 1 — Instalar o JMeter
- Acessar o endereço https://jmeter.apache.org/download_jmeter.cgi
- Instalar o apacheJmeter de Binaries

✅ PASSO 2 — Instalar o JMeter Plugins Manager
- Acessar o endereço https://jmeter.apache.org/download_jmeter.cgi
- Instalar o JMeter Plugins Manager
- Ir em apache-jmeter-5.6.3 > lib > ext
- Colar o jar do JMeter Plugins Manager na pasta ext

✅ PASSO 3 — Instalar o Custom Thread Groups
- Inicializar o JMeter
- Acessar Opções > Plugin Manager
- Buscar por Custom Thread Groups
- Instalar e reiniciar o Custom Thread Groups

✅ PASSO 4 — Mão na Massa
- Baixar o AgileBankPerformance.jmx
- Crie a pasta reports
- E crie uma nova pasta dentro dessa de reports com nome dashboard (Para facilitar o report mais tarde)
- Inicializar o Jmeter
- Importar o arquivo jmx para o Jmeter
- Feito isso só configurar sua rampa e executar o teste de performance!

✅ PASSO 5 — Gerar Relatório
- Ao executar ele já deve salvar no relatório agregado do jmx
- Mas para gerar um relatório mais conciso, abra o bloco de notas
- Informe o seguinte script:
"@echo off
REM Caminho do JMeter (coloque o seu se for diferente)
set JMETER_HOME=C:\apache-jmeter-5.6.3

REM Arquivo JTL dentro da pasta reports
set RESULT_FILE=reports\results.jtl

REM Pasta onde o dashboard será gerado
set REPORT_FOLDER=reports\dashboard

"%JMETER_HOME%\bin\jmeter.bat" -g "%RESULT_FILE%" -o "%REPORT_FOLDER%"

echo -----------------------------------------
echo Relatorio gerado em: %REPORT_FOLDER%\index.html
echo -----------------------------------------
pause"

- Feito isso só salvar o arquivo como .bat no seu bin com o nome de sua preferência como "gerador_relatorio"
- Execute o arquivo .bat
- Após isso só acessar bin > reports > dashboard
- Executar o index html
- Terá seu relatório com gráfico!
