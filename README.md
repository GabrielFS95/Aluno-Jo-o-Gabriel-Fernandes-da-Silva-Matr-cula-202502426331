# Aluno-Jo-o-Gabriel-Fernandes-da-Silva-Matr-cula-202502426331

import pandas as pd
import numpy as np

# ── 1. CARREGAR O DATASET ──────────────────────────────
df = pd.read_csv("livros.csv", sep=";")
print(f"Shape: {df.shape}")  # (linhas, colunas)

# ── 2. EXPLORAÇÃO INICIAL ─────────────────────────────
print(df.head())
print(df.info())
print(df.describe())
print(df.isnull().sum())

# ── 3. LIMPEZA ────────────────────────────────────────
# Preencher nulos de 'ano' com a mediana
mediana_ano = df["ano"].median()
df["ano"] = df["ano"].fillna(mediana_ano).astype(int)

# Remover livros com 0 páginas
df_limpo = df[df["paginas"] > 0].copy()

# ── 4. TRANSFORMAÇÃO ──────────────────────────────────
def faixa_paginas(n):
    if n < 150: return "Curto"
    elif n <= 350: return "Médio"
    else: return "Longo"

df_limpo["faixa_paginas"] = df_limpo["paginas"].apply(faixa_paginas)
df_limpo["decada"] = (df_limpo["ano"] // 10) * 10

# ── 5. ANÁLISE ────────────────────────────────────────
# TODO: adicione seus GroupBys e análises aqui

# ── 6. EXPORTAR ───────────────────────────────────────
df_limpo.to_excel("livros_analisados.xlsx", index=False)
print("✅ Arquivo exportado com sucesso!")
