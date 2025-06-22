Siga os passos abaixo para configurar o ambiente e executar o pipeline experimental.

## 1. Pré-requisitos

- **Python 3.12** (recomendado)
- **Git**
- **GPU** com pelo menos 15GB de memória (ex: Google Colab T4) para fine-tuning. Para avaliação, CPU é suficiente (mais lento).

## 2. Clonando o Repositório

```bash
git clone git@github.com:lcs147/nlp-tp4.git
cd nlp-tp4
```

## 3. Instalando as Dependências

O projeto utiliza ambiente virtual para garantir versões exatas dos pacotes.

**Usando pip:**
```bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

**Ou usando pipenv:**
```bash
pip install pipenv
pipenv install
pipenv shell
```

> **Obs:** Se for utilizar GPU, certifique-se de que os drivers CUDA estejam instalados e compatíveis com as versões do PyTorch e bitsandbytes.

## 4. Download dos Dados

- Baixe o **Spider dataset** em [https://yale-lily.github.io/spider](https://yale-lily.github.io/spider) e coloque os arquivos em `datasets/spider_data/`.
- Os dados do **MMLU** são baixados automaticamente via Hugging Face Datasets.

## 5. Execução dos Scripts

Execute os scripts na ordem abaixo para reproduzir o pipeline:

1. **Pré-processamento dos dados:**
    ```bash
    python scripts/0_preparando_dados.py
    ```
    (Gera arquivos processados em `datasets/`)

2. **Fine-tuning supervisionado com LoRA:**
    ```bash
    python scripts/1_fine-tuning.py
    ```
    (Checkpoints salvos em `checkpoints/loras/`)

3. **Cálculo do baseline na tarefa-alvo:**
    ```bash
    python scripts/2_calculando_baseline.py
    ```
    (Resultados exibidos no terminal)

4. **Avaliação customizada com DeepEval:**
    ```bash
    python scripts/3_avaliacao_customizada.py
    ```
    (Resultados exibidos no terminal)

5. **Avaliação de generalização no MMLU:**
    ```bash
    python scripts/4_analise_mmlu.py
    ```
    (Resultados exibidos no terminal)

## 6. Resultados

Os resultados intermediários são salvos em `checkpoints/`.  
Os resultados finais (acurácia, desvio padrão) são exibidos na saída dos scripts.

## 7. Observações

- Todos os seeds aleatórios foram fixados em 42 para garantir reprodutibilidade.
- Se estiver usando Google Colab, ajuste os caminhos dos arquivos conforme necessário.
- O notebook `experiments_runner_colab.ipynb` guarda as saídas dos experimentos rodados.
- O arquivo `./relatorio_latex/results.txt` guarda todos os resultados utilizados no relatório.
- O relatório está disponível em `./relatorio_latex/main.pdf`.