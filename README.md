# Projeto Aurora Siger - Sistema de Monitoramento Pré-Decolagem 

Este projeto integra engenharia de sistemas aeroespaciais com ciência de dados. O **Aurora Siger** é um software de monitoramento que simula a telemetria crítica de uma aeronave, validando parâmetros de segurança e realizando cálculos de autonomia energética em tempo real para suporte à decisão de lançamento.

## Funcionalidades Principais
* **Análise Preditiva de Autonomia:** Cálculo de energia bruta (kWh) e autonomia residual pós-decolagem.
* **Processamento em Lote (Batch):** Simulação de 100 missões simultâneas para geração de estatísticas de confiabilidade.
* **Persistência de Dados:** Exportação automática de um dataset completo em formato `.csv` para auditoria e histórico.

---

## Parâmetros Técnicos e Escopo de Segurança

O sistema utiliza os seguintes *thresholds* baseados em normas internacionais para autorização de voo:

| Parâmetro | Unidade | Intervalo Seguro | Norma/Referência |
| :--- | :--- | :--- | :--- |
| **Temp. Interna** | °C | 21.0 - 25.0 | ASHRAE Standard 55 |
| **Temp. Externa** | °C | -10.0 - 38.0 | NASA GEVS |
| **Pressão Tanques** | bar | 200 - 300 | Sutton (Rocket Prop.) |
| **Nível de Energia**| % | ≥ 80.0 | Premissa Operacional |
| **Sistemas Críticos**| bin | 1 (Nominal) | Requisito de Missão |

###  Equações de Engenharia Elétrica 
O software aplica as seguintes fórmulas para validar a viabilidade energética:
1.  **Energia Bruta (kWh):** $$Capacidade\ Total \times (Nivel\ Energia / 100)$$
2.  **Autonomia Residual:** $$(Energia\ Bruta \times Eficiência) - Consumo\ Estimado$$
    * *Critério de Segurança:* A decolagem só é autorizada se a Autonomia Residual for **> 10 kWh**.

---

##  Tecnologias e Bibliotecas
* **Python 3.x**: Núcleo lógico e estrutural.
* **Pandas**: Estruturação de dados em DataFrames e manipulação de arquivos CSV.
* **NumPy**: Suporte para operações matemáticas e cálculos vetoriais.
* **Jupyter/Python Notebook**: Ambiente de desenvolvimento e exibição de tabelas.

---

##  Funcionamento do Algoritmo

1.  **Geração Estocástica**: O script simula 100 registros de telemetria com **78% de probabilidade de sucesso** (missões nominais) e 22% de anomalias críticas para testes de estresse.
2.  **Validação de Vetores**: Uma função de checklist verifica cada dado individualmente contra os limites de segurança (Critério de Falha Única).
3.  **Processamento de Dataset**: O sistema compila os resultados em uma tabela, calculando a taxa de sucesso global e a média de autonomia da frota simulada.
4.  **Veredito de Missão**: O status final é gerado com foco na missão atual, exibindo o diagnóstico detalhado de todos os sensores e o balanço energético.

---

##  Exemplo de Relatório de Saída
```text
=======================================================
        SISTEMA DE MONITORAMENTO PRÉ-DECOLAGEM         
=======================================================
Temp Int       :    23.50 °C    -> [OK]
Energia        :    92.00 %     -> [OK]
Pressao        :   250.00 bar   -> [OK]
-------------------------------------------------------
Energia Bruta  :    46.00 kWh
Autonomia Final:    28.70 kWh
-------------------------------------------------------
Taxa de Sucesso da Missão: 84%
STATUS FINAL: [SISTEMAS NOMINAIS - PRONTO PARA DECOLAR]
=======================================================