---
title: "Pipeline Automatizado em Python para Diagnóstico de Qualidade de Energia"
date: 2026-07-28
draft: false

description: "Desenvolvimento de uma solução em Python para automatizar o tratamento ETL, análise estatística e diagnóstico normativo de Qualidade de Energia Elétrica (QEE)."

categories:
  - Ciência de Dados
  - Engenharia Elétrica

tags:
  - Python
  - Pandas
  - NumPy
  - Matplotlib
  - LaTeX
  - ETL
  - Qualidade de Energia
  - Automação
---

<!-- METRICAS DE IMPACTO (KPI GRID) -->
<div class="grid grid-cols-2 md:grid-cols-4 gap-4 my-8">
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-blue-400">1.666</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Amostras Temporais</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-blue-400">51,39 kW</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Demanda de Pico</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-emerald-400">0,949</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">FP Médio Global</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-emerald-400">&lt; 3s</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Tempo de Pipeline</span>
  </div>
</div>

<!-- CARD DO REPOSITORIO GITHUB -->
<div class="my-8 p-4 rounded-xl bg-[#111827] border border-gray-800 flex flex-col sm:flex-row items-center justify-between gap-4">
  <div class="flex items-center gap-3">
    <div class="p-2.5 rounded-lg bg-blue-500/10 text-blue-400 border border-blue-500/20">
      <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
    </div>
    <div>
      <h4 class="text-white font-bold text-sm mb-0.5">Código-Fonte do Projeto</h4>
      <p class="text-gray-400 text-xs m-0">Acesse a arquitetura completa em Python, scripts ETL e gerador LaTeX no GitHub.</p>
    </div>
  </div>
  <a href="https://github.com/SEU-USUARIO/SEU-REPOSITORIO" target="_blank" class="px-4 py-2 rounded-lg bg-blue-600 hover:bg-blue-500 text-white font-semibold text-xs transition-colors whitespace-nowrap">
    Ver Repositório no GitHub →
  </a>
</div>

---

### 📋 Ficha Técnica do Projeto

| Parâmetro | Especificação / Tecnologias |
| :--- | :--- |
| **Domínio de Aplicação** | Qualidade da Energia Elétrica (QEE), Eficiência & Analytics |
| **Nível de Aplicação** | Engenharia de Dados & Diagnóstico de Negócios / Ativos |
| **Ferramentas Computacionais** | Python, Pandas, NumPy, Matplotlib, OpenPyXL, LaTeX |
| **Arquitetura da Solução** | Pipeline ETL Modular + Análise Normativa (PRODIST/ANEEL) + Report Automation |
| **Métricas Avaliadas** | Perfil de Demanda, Fator de Potência, THD<sub>V</sub>, THD<sub>I</sub>, Harmônicas Triplen |

## 01. Contexto & Desafio de Negócio

Campanhas de monitoramento de Qualidade de Energia Elétrica (QEE) geram milhares de séries temporais que costumam ser analisadas manualmente em planilhas. Esse processo manual é lento, vulnerável a falhas de digitação e ineficiente para decisões operacionais rápidas.

A meta deste projeto foi desenhar uma **solução automatizada em Python** capaz de receber logs brutos de analisadores trifásicos, consolidar os indicadores técnicos e financeiros e entregar diagnósticos de alta precisão em **menos de 3 segundos**.

> **Fluxo de Valor:** Arquivo Bruto (.xlsx) ➔ Ingestão & Sanitização ETL ➔ Processamento Vetorial ➔ Dashboard Executivo + Relatório TeX Nativo

### Modelagem Matemática do Pipeline

O pipeline executa o cálculo vetorial contínuo da série temporal ($1.666$ amostras em $138{,}75$ horas de medição) para derivar as grandezas fundamentais da instalação:

<!-- CARD ESTILIZADO DE EQUAÇÕES MATEMÁTICAS -->
<div class="my-6 p-6 rounded-xl bg-[#111827] border border-gray-800 font-mono text-sm md:text-base text-gray-200 shadow-inner space-y-3 text-center">
  <div>
    <span class="text-blue-400 font-bold">Potência Aparente:</span> S(t) = √(P(t)² + Q(t)²)
  </div>
  <div>
    <span class="text-amber-400 font-bold">Fator de Potência Real:</span> FP(t) = P(t) / S(t)
  </div>
  <div>
    <span class="text-purple-400 font-bold">Distorção Harmônica:</span> THD_V = (√(∑ Vₙ²) / V₁) · 100%
  </div>
  <div class="pt-2 border-t border-gray-800/80 max-w-md mx-auto">
    <span class="text-emerald-400 font-bold">Dimensionamento Capacitivo:</span> Q_c = P_pico · (tan φ₁ - tan φ₂)
  </div>
</div>

---

## 02. Solução Arquitetada

Para garantir reprodutibilidade e desempenho de nível corporativo, o pipeline foi divido em quatro módulos:

1. **ETL & Sanitização de Datas Legadas:** Ingestão de planilhas complexas com remoção de colunas nulas e conversão do formato de data serial do Excel (`origin="1899-12-30"`) para objetos `datetime` padronizados.
2. **Processamento Vetorial e Diagnóstico Normativo:** Cálculos estatísticos globais e diários, varredura de afundamentos momentâneos de tensão (VTCDs) e validação dos limites do **Módulo 8 do PRODIST (ANEEL)**.
3. **Engine de Visualização Executiva:** Exportação automatizada dos gráficos operacionais em **250 DPI** com layout padronizado.
4. **Gerador LaTeX Automatizado:** Formatação de tabelas normativas prontas para relatórios técnicos em `.tex`, convertendo separadores decimais para o padrão PT-BR (vírgula).

---

## 03. Galeria de Resultados & Diagnóstico Executivo

### 🔹 Perfil Temporal de Demanda e Curva de Carga
A curva de carga evidencia o comportamento operacional da instalação. Nota-se um consumo de base (*baseload*) entre 3 kW e 5 kW nos finais de semana e picos operacionais bem definidos nos dias úteis, atingindo a **demanda máxima de 51,39 kW** no dia 22/05 às 15:21.

<!-- FIGURA 1: CURVA DE CARGA -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/qee/curvacarga.png" alt="Curva de Carga do Bloco" class="w-full rounded-lg mx-auto block" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 1: Curva de Carga temporal com registro da demanda máxima de 51,39 kW e consumo total de 1.507,71 kWh no período.
  </p>
</div>

---

### 🔹 Análise de Eficiência Energética e Fator de Potência

Embora o Fator de Potência médio global seja adequado (**0,949**), a análise contínua revelou **298 registros abaixo do limite regulatório de 0,92**, especialmente durante madrugadas e horários de baixa carga. 

Para adequar a instalação no momento de demanda máxima (**P = 51,39 kW**, **FP<sub>1</sub> = 0,934**), o algoritmo dimensionou pontualmente um **banco capacitivo de 2,85 kvar** para atingir a meta de **FP<sub>2</sub> = 0,95**, evitando investimentos excessivos.



<!-- FIGURA 2: FATOR DE POTÊNCIA -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/qee/fatorpotencia.png" alt="Fator de Potência ao Longo da Medição" class="w-full rounded-lg mx-auto block" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 2: Monitoramento contínuo do FP com linhas de referência normativas (0,92 regulatório e 0,95 meta).
  </p>
</div>

---

### 🔹 Balanço Diário de Consumo Energético
A consolidação vetorial por data permite identificar rapidamente os dias de maior atividade operacional, destacando a terça-feira (26/05) com o maior consumo acumulado do período (**422,12 kWh**).

<!-- FIGURA 3: ENERGIA DIÁRIA -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/qee/energiadiaria.png" alt="Energia Ativa Diária Estimada" class="w-full rounded-lg mx-auto block" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 3: Consumo de energia ativa diário acumulado (Total do período: 1.507,71 kWh).
  </p>
</div>

---

### 🔬 Diagnóstico Avançado de Qualidade de Onda (Deep-Dive Técnico)

A avaliação da qualidade de onda revelou inconformidades regulatórias importantes. A linha de base da Distorção Harmônica Total de Tensão (**THD<sub>V</sub>**) manteve-se constante em torno de **18%**, superando o limite de **10%** estabelecido pelo Módulo 8 do PRODIST (ANEEL) para redes de baixa tensão. Além disso, foram registrados picos de transientes de até 80% na fase **V<sub>3</sub>**, associados a um afundamento momentâneo severo (**147,20 V**).

<!-- FIGURA 4: THD TENSAO -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/qee/thdtensao.png" alt="Distorção Harmônica Total de Tensão" class="w-full rounded-lg mx-auto block" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 4: THD<sub>V</sub> contínuo indicando não-conformidade com o padrão PRODIST/ANEEL (10%).
  </p>
</div>

A decomposição harmônica de corrente aponta a causa raiz da distorção: elevada presença de **9ª ordem (4,42 A)** e componentes *triplen* (3ª e 7ª ordens), características do uso massivo de cargas não lineares monofásicas e fontes chaveadas na instalação.

<!-- FIGURA 5: HARMONICAS DE CORRENTE -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/qee/harmonicascorrente.png" alt="Componentes Harmônicas de Corrente" class="w-full rounded-lg mx-auto block" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 5: Espectro harmônico médio de corrente por fase com destaque para ordens ímpares triplen.
  </p>
</div>

## 04. Impacto Financeiro & Operacional



* **Redução drástica do tempo de análise:** Processamento completo do laudo em **menos de 3 segundos** (redução de mais de 98% em relação ao fluxo manual em Excel).
* **Decisão de CAPEX Baseada em Dados:** O dimensionamento preciso (**Q<sub>c</sub> = 2,85 kvar**) evitou a aquisição desnecessária de bancos capacitivos sobredimensionados.
* **Mitigação de Riscos de Multa:** Identificação detalhada dos 298 períodos de inconformidade do FP para programação de correção automatizada.
* **Reprodutibilidade Científica:** Eliminação de erros humanos de digitação através da automação direta de relatórios em código LaTeX.

---

## 05. Código-Fonte & Implementação

Abaixo apresenta-se o trecho do pipeline responsável pelo carregamento, sanitização de datas legadas do Excel e exportação automatizada das tabelas formatadas em LaTeX:

```python
# ==========================================================
# PIPELINE DE QUALIDADE DE ENERGIA - ETL & REPORT AUTOMATION
# ==========================================================

import pandas as pd
import numpy as np

def carregar_e_sanitizar(caminho_excel: str) -> pd.DataFrame:
    """Carrega dados brutos, remove colunas fantasma e trata datas legadas."""
    df = pd.read_excel(caminho_excel)
    df = df.loc[:, ~df.columns.astype(str).str.startswith("Unnamed")]
    
    # Tratamento de data em formato serial do Excel (origin 1899-12-30)
    if np.issubdtype(df["Time"].dtype, np.number):
        df["DataHora"] = pd.to_datetime(df["Time"], unit="D", origin="1899-12-30")
    else:
        df["DataHora"] = pd.to_datetime(df["Time"], errors="coerce")
        
    return df.dropna(subset=["DataHora"]).sort_values("DataHora").reset_index(drop=True)

def exportar_tabela_latex(df_stats: pd.DataFrame, arquivo_saida: str):
    """Gera bloco de código TeX com separador decimal PT-BR (vírgula)."""
    linhas = ["\\begin{tabular}{lrrr}", "\\hline", "Grandeza & Média & Mínimo & Máximo \\\\", "\\hline"]
    for _, r in df_stats.iterrows():
        med, mini, maxi = [f"{v:.2f}".replace('.', ',') for v in [r['Media'], r['Minimo'], r['Maximo']]]
        linhas.append(f"{r['Grandeza']} & {med} & {mini} & {maxi} \\\\")
    linhas.extend(["\\hline", "\\end{tabular}"])
    
    with open(arquivo_saida, "w", encoding="utf-8") as f:
        f.write("\n".join(linhas))

```       
        
## 06. Competências Demonstradas

* **Python & Engenharia de Software Aplicada**
* **Tratamento e Análise Vetorial de Séries Temporais** (Pandas / NumPy)
* **Visualização de Dados Executiva** (Matplotlib)
* **Análise Normativa de Qualidade de Energia** (PRODIST / ANEEL)
* **Automação de Relatórios de Engenharia** (LaTeX)
* **Modelagem e Dimensionamento Elétrico de Ativos**

---

## Conclusão

Este projeto reflete o valor da **Ciência de Dados aplicada à Engenharia Elétrica**. Ao automatizar tarefas repetitivas de baixo valor agregado, o pipeline garante diagnósticos precisos, ágeis e respaldados por normas regulatórias, permitindo que a tomada de decisão seja rápida, segura e fundamentada em dados.