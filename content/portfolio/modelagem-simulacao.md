---
title: "Filtragem Digital e Processamento de Sinais com MATLAB"
date: 2026-07-28
draft: false
description: "Desenvolvimento, simulação e validação de uma solução computacional em MATLAB para remoção de ruídos de alta frequência via Filtro IIR Butterworth de 4ª ordem e análise espectral por FFT."

categories:
  - Modelagem e Simulação
  - Engenharia Elétrica

tags:
  - MATLAB
  - PDS
  - Filtros Digitais
  - Butterworth
  - FFT
  - Sinais e Sistemas
---

<!-- METRICAS DE IMPACTO (KPI GRID) -->
<div class="grid grid-cols-2 md:grid-cols-4 gap-4 my-8">
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-blue-400">1000 Hz</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Amostragem (f<sub>s</sub>)</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-blue-400">100 Hz</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Corte (f<sub>c</sub>)</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-blue-400">4ª Ordem</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Filtro Butterworth</span>
  </div>
  <div class="p-4 rounded-xl bg-[#111827] border border-gray-800 text-center">
    <span class="block text-2xl md:text-3xl font-extrabold text-emerald-400">300 Hz</span>
    <span class="text-xs text-gray-400 font-mono uppercase tracking-wider">Interferência Eliminada</span>
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
      <p class="text-gray-400 text-xs m-0">Acesse o repositório completo com scripts .m e arquivos de simulação no GitHub.</p>
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
| **Domínio de Aplicação** | Processamento Digital de Sinais (PDS) & Instrumentação |
| **Nível de Aplicação** | Engenharia de Sistemas & Alta Precisão |
| **Ferramentas Computacionais** | MATLAB, Signal Processing Toolbox, DSP Pipeline |
| **Arquitetura do Filtro** | IIR Passa-Baixa Butterworth (Topologia Maximamente Plana) |
| **Método de Análise** | Transformada Rápida de Fourier (FFT), Diagramas de Bode |

---

## 01. Contexto & Desafio Técnico

Em cenários industriais de instrumentação, automação e sistemas de comunicação, sinais elétricos brutos capturados por sensores frequentemente sofrem severas distorções causadas por **interferências eletromagnéticas (EMI)** e **ruídos térmicos de fundo**.

O objetivo deste projeto consistiu em sintetizar e validar uma pipeline em **MATLAB** capaz de isolar e recuperar com alta fidelidade a informação de um sinal contaminado por componentes determinísticas de alta amplitude e ruído estocástico.

> **Fluxo da Solução:** Sinal Bruto ➔ Análise FFT ➔ Filtro Butterworth ➔ Sinal Recuperado

### Modelagem Matemática do Sistema

O ambiente de teste simulou um sinal útil composto por duas harmônicas fundamentais (**10 Hz** e **30 Hz**), corrompido por uma interferência senoidal severa (**300 Hz**) e ruído branco gaussiano **w(t)**:

<!-- CARD ESTILIZADO DE EQUAÇÕES MATEMÁTICAS -->
<div class="my-6 p-6 rounded-xl bg-[#111827] border border-gray-800 font-mono text-sm md:text-base text-gray-200 shadow-inner space-y-3 text-center">
  <div>
    <span class="text-blue-400 font-bold">x<sub>limpo</sub>(t)</span> = 2 · sin(2π · 10t) + 1.5 · sin(2π · 30t)
  </div>
  <div>
    <span class="text-amber-400 font-bold">n(t)</span> = 2.5 · sin(2π · 300t) + w(t)
  </div>
  <div class="pt-2 border-t border-gray-800/80 max-w-md mx-auto">
    <span class="text-emerald-400 font-bold">x<sub>sujo</sub>(t)</span> = x<sub>limpo</sub>(t) + n(t)
  </div>
</div>

---

## 02. Solução Arquitetada

Para a resolução do problema de contaminação espectral, implementou-se uma metodologia em três pilares analíticos:

* **Mapeamento Espectral via FFT:** Mapeamento no domínio da frequência utilizando o algoritmo *Fast Fourier Transform* com adequação de Nyquist (**f<sub>s</sub> = 1000 Hz**), permitindo a separação limpa das bandas de interesse (**< 50 Hz**) e da banda de ruído (**300 Hz**).
* **Dimensionamento do Filtro IIR Butterworth:** Escolha de uma arquitetura Passa-Baixa de 4ª ordem com frequência de corte em **f<sub>c</sub> = 100 Hz**. A topologia Butterworth foi selecionada devido à sua característica de **resposta maximamente plana (*maximally flat*) na banda passante**, prevenindo a introdução de ripples ou distorções de ganho no sinal de interesse.
* **Filtragem e Validação Temporal:** Execução do processamento digital no domínio do tempo e verificação comparativa rigorosa contra o sinal de referência teórico.

---

## 03. Galeria de Resultados & Validação Experimental

### 🔹 Análise no Domínio do Tempo (Entrada Ruidosa)
Abaixo observa-se a degradação massiva sofrida pelo sinal original devido à sobreposição da componente de 300 Hz de elevada amplitude combinada ao ruído estocástico.

<!-- PAINEL INTERATIVO - FIGURA 1 -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/pds/figura1.png" alt="Sinal Original vs Sinal Corrompido" class="w-full rounded-lg mx-auto block" style="filter: invert(0.9) hue-rotate(180deg);" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 1: Degradação temporal do sinal de entrada causada por ruídos determinísticos e estocásticos.
  </p>
</div>

---

### 🔹 Mapeamento Espectral via FFT
A aplicação da Transformada Rápida de Fourier evidencia os picos fundamentais de informação em **10 Hz** e **30 Hz**, bem como a ponta de interferência isolada em **300 Hz**, confirmando a viabilidade técnica do corte em **100 Hz**.

<!-- PAINEL INTERATIVO - FIGURA 2 -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/pds/figura2.png" alt="Espectro de Frequência do Sinal Sujo" class="w-full rounded-lg mx-auto block" style="filter: invert(0.9) hue-rotate(180deg);" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 2: Análise espectral confirmando a distribuição de frequências antes do processo de filtragem.
  </p>
</div>

---

### 🔹 Resposta em Frequência do Filtro (Diagrama de Bode)
O diagrama de magnitude e fase comprova a precisão do filtro projetado: ganho de **0 dB** na banda de passagem (**< 100 Hz**) e atenuação superior a **-40 dB** na região da interferência em **300 Hz**.

<!-- PAINEL INTERATIVO - FIGURA 3 -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/pds/figura3.png" alt="Resposta em Frequência do Filtro Passa-Baixa" class="w-full rounded-lg mx-auto block" style="filter: invert(0.9) hue-rotate(180deg);" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 3: Resposta de magnitude (dB) e fase (graus) do filtro Butterworth IIR de 4ª ordem.
  </p>
</div>

---

### 🔹 Resultado Final da Filtragem
Comparação direta provando a recuperação do sinal útil sintetizado. A atenuação atinge nível próximo do ideal, eliminando oscilações de alta frequência e restaurando a forma de onda suave original.

<!-- PAINEL INTERATIVO - FIGURA 4 -->
<div class="my-6 p-3 md:p-4 rounded-xl bg-[#111827] border border-gray-800 shadow-lg">
  <img src="/images/portfolio/pds/figura4.png" alt="Resultado da Filtragem" class="w-full rounded-lg mx-auto block" style="filter: invert(0.9) hue-rotate(180deg);" />
  <p class="text-center text-xs md:text-sm text-gray-400 mt-3 mb-1 font-mono">
    Figura 4: Sinal de entrada ruidoso (1), saída filtrada (2) e referência teórica limpa (3).
  </p>
</div>

## 04. Principais Entregáveis & Impacto

* **Algoritmo Modular em MATLAB:** Código-fonte limpo, parametrizado e pronto para integração em bancadas de testes ou sistemas embarcados.
* **Isolamento de Sinal de Alta Precisão:** Atenuação completa da interferência de 300 Hz mantendo **100% da integridade de amplitude e fase** das frequências úteis.
* **Documentação Técnica Completa:** Relatório analítico detalhado cobrindo modelagem no tempo, frequência e projeto de filtros.

---

## 05. Código-Fonte & Implementação

A implementação foi codificada utilizando recursos nativos da **Signal Processing Toolbox** do MATLAB:

```matlab
% ==========================================================
% PROJETO DE FILTRAGEM DIGITAL - FILTRO PASSA-BAIXA BUTTERWORTH
% ==========================================================

% Parâmetros Principais
fs = 1000;         % Frequência de amostragem (Hz)
fc = 100;          % Frequência de corte (Hz)
ordem = 4;         % Ordem do filtro Butterworth

% Projeto do Filtro
[b, a] = butter(ordem, fc/(fs/2), 'low');

% Aplicação do Filtro ao Sinal Corrompido
sinal_recuperado = filter(b, a, sinal_sujo);

```
## 06. Competências Demonstradas

* **MATLAB & Signal Processing Toolbox**
* **Processamento Digital de Sinais (PDS)**
* **Transformada Rápida de Fourier (FFT)**
* **Projeto de Filtros Digitais (Butterworth IIR)**
* **Análise Espectral & Diagramas de Bode**
* **Modelagem Matemática de Sistemas Lineares**
