# Projeto Aurora Siger - Sistema de Monitoramento Pré-Decolagem 

Este projeto faz parte de uma atividade integradora focada em engenharia de sistemas aeroespaciais. O objetivo é simular a telemetria crítica de uma aeronave e validar se os parâmetros de segurança permitem uma decolagem segura ou se a missão deve ser abortada.

## Sobre o Projeto

O **Aurora Siger** é um software de monitoramento que utiliza lógica probabilística para simular sensores em tempo real. Ele verifica variáveis fundamentais baseadas em normas internacionais de segurança e conforto térmico.

### Parâmetros de Verificação (Escopo)
| Parâmetro | Intervalo Seguro | Norma/Referência |
| :--- | :--- | :--- |
| **Temperatura Interna** | 21°C - 25°C | ASHRAE Standard 55 |
| **Temperatura Externa** | -10°C - 38°C | NASA GEVS |
| **Nível de Energia** | ≥ 80% | Premissa Operacional |
| **Pressão dos Tanques** | 200 - 300 bar | Sutton (Rocket Propulsion) |
| **Integridade/Módulos** | Binário (1) | Requisito de Sistemas |

---

## Tecnologias Utilizadas

* **Python 3.x**: Linguagem principal para a lógica do script.
* **Jupyter Notebook (.ipynb)**: Ambiente de desenvolvimento e documentação.
* **Biblioteca `random`**: Utilizada para simular a variação dos sensores.

---

## Funcionamento do Algoritmo

O sistema opera com uma **probabilidade de 90% de sucesso**. 
1.  **Simulação**: O script gera números aleatórios dentro ou fora dos escopos de segurança.
2.  **Validação**: Uma função de checklist verifica cada dado individualmente.
3.  **Veredito**: Se qualquer parâmetro estiver fora do limite, o sistema emite o alerta `DECOLAGEM ABORTADA`.

### Exemplo de Execução:
```text
=======================================================
        SISTEMA DE MONITORAMENTO PRÉ-DECOLAGEM         
=======================================================
Temp Int       :   22.77 °C    -> [OK]
Temp Ext       :   -0.95 °C    -> [OK]
Energia        :   83.14 %     -> [OK]
Pressao        :  206.97 bar   -> [OK]
Integridade    :       1       -> [OK]
Modulos        :       1       -> [OK]
-------------------------------------------------------
          STATUS FINAL: [PRONTO PARA DECOLAR]          
=======================================================