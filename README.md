# SAE — Sistema de Aprovação de Empréstimos (ML + Streamlit)

Aplicação de **classificação** para prever a **aprovação de empréstimos** a partir de dados cadastrais e histórico de crédito.  
O repositório inclui **EDA**, **treinamento do modelo** e um app em **Streamlit** para inferência.

---

## 🎯 Problema de negócio

Em processos de crédito, decisões manuais podem ser lentas e inconsistentes.  
Este projeto usa Machine Learning para estimar automaticamente se um empréstimo tende a ser **aprovado** ou **rejeitado**, apoiando triagem e priorização.

---

## ✅ Entregáveis

- **Notebook 01 — Análise e Tratamento** (`notebooks/01_analysis.ipynb`)
- **Notebook 02 — Treinamento e Predição** (`notebooks/02_predction.ipynb`)
- **App Streamlit** (`app.py`)
- **Artefato do modelo** (`models/maquina_preditiva.pkl`)
- **Dados** (`data/raw/` e `data/processed/`)

---

## 🧠 Como o app faz a predição (para manter consistência)

O app:

1. **Carrega** o modelo treinado (`models/maquina_preditiva.pkl`).
2. **Converte** categorias para numérico:
   - `sexo`: Masculino → 0 | Feminino → 1
   - `estado_civil`: Solteiro(a) → 0 | Casado(a) → 1
   - `historico_credito`: Débitos Pendentes → 0 | Sem Débitos → 1
3. **Reescala** o empréstimo: `emprestimo = emprestimo / 1000`
4. Envia para o modelo na ordem:
   `[[sexo, estado_civil, renda, emprestimo, historico_credito]]`
5. Retorna:
   - `0` → **Rejeitado**
   - `1` → **Aprovado**

> ⚠️ Se você alterar essas regras no notebook, mantenha o mesmo padrão no app (ou coloque tudo num Pipeline do sklearn).

---

## 🗂️ Estrutura recomendada do repositório

```
.
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── data/
│   ├── raw/
│   │   └── clientes.csv
│   └── processed/
│       └── clientes_tratado.csv
├── notebooks/
│   ├── 01_analysis.ipynb
│   └── 02_predction.ipynb
└── models/
    └── maquina_preditiva.pkl
```

---

## ⚙️ Como rodar localmente

### 1) Criar ambiente e instalar dependências

```bash
python -m venv .venv

# Windows:
.venv\Scripts\activate

# Linux/Mac:
source .venv/bin/activate

pip install -r requirements.txt
```

### 2) Rodar os notebooks (opcional, para treinar/gerar artefatos)

1. Rode `notebooks/01_analysis.ipynb` para tratar os dados e gerar/validar `data/processed/clientes_tratado.csv`
2. Rode `notebooks/02_predction.ipynb` para treinar o modelo e salvar `models/maquina_preditiva.pkl`

> Se `models/maquina_preditiva.pkl` não existir, o app não abrirá (ou não conseguirá predizer).

---

## 🖥️ Rodar o app Streamlit

Na raiz do projeto:

```bash
streamlit run app.py
```
## 👩‍💻 Autoria

CDPRO / **Daniela de David**
