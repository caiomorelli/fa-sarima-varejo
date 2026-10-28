# SARIMA no comércio varejista: Amapá

Exercício da disciplina **Financial Analytics** do PADS Insper: modelagem SARIMA do índice de volume de vendas do **comércio varejista ampliado** do Amapá, a partir da PMC (Pesquisa Mensal do Comércio) do IBGE.

📊 **Relatório:** https://caiomorelli.github.io/fa-sarima-varejo/

## Dados

- **Fonte:** PMC/IBGE, índice de volume de vendas do varejo ampliado (inclui veículos e materiais de construção), por Unidade da Federação.
- **Período:** mensal, de jan/2004 a fev/2026.
- **Base:** 2022 = 100, sem ajuste sazonal.

## O que o relatório cobre

1. Análise descritiva: série em nível, decomposição STL, padrão sazonal por mês e amplitude sazonal por ano.
2. Diferenciação (regular, sazonal e as duas combinadas) com ACF, PACF e testes ADF e KPSS.
3. Estimativa do número de diferenças com `ndiffs` e `nsdiffs`.
4. Comparação entre os modelos candidatos da análise visual e o `AutoARIMA(season_length=12)`, por AICc.
5. Diagnóstico dos resíduos: gráficos, ACF, normalidade e teste de Ljung-Box.
6. Previsão de 24 meses à frente, com intervalos de 80% e 95%.
7. Discussão dos resultados e comparação com outras UFs.

## Resultado

O modelo final é o **SARIMA(1,0,0)(0,1,1)[12] com drift**. Esse modelo tem o menor AICc entre os modelos comparáveis, resíduos compatíveis com ruído branco e uma previsão que mantém o crescimento observado no histórico da série.

## Como reproduzir

Requisitos: [uv](https://docs.astral.sh/uv/) e [Quarto](https://quarto.org/).

```bash
git clone https://github.com/caiomorelli/fa-sarima-varejo.git
cd fa-sarima-varejo
uv sync
uv run quarto render template-exercicio-sarima.qmd
```

O `uv sync` cria o `.venv` com as dependências do `pyproject.toml`. A renderização gera o `index.html`, que é o arquivo servido pelo GitHub Pages.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `template-exercicio-sarima.qmd` | Código e análise (fonte do relatório) |
| `index.html` | Relatório renderizado, publicado no GitHub Pages |
| `pyproject.toml` / `uv.lock` | Dependências do projeto, gerenciadas pelo `uv` |
