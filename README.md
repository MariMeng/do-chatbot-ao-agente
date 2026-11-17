# Do Chatbot ao Agente

### Criando seu primeiro Agente de Inteligência Artificial com Python

Material do minicurso ministrado em **10/11/2026, das 14h às 18h**, por mim.
Evento/local: Semana Acadêmica de Computação — UNIR, Porto Velho

O minicurso começa com uma pergunta simples a um modelo de linguagem. Termina com um **agente assistente de estudos**, o **Estudaí**, que:

- consulta a Wikipédia;
- faz contas com precisão;
- sabe que dia é hoje;
- organiza tarefas e monta um plano de estudo com Pomodoros.

Tudo roda no **Google Colab** com a **API do Gemini** (biblioteca oficial `google-genai`). Não é preciso instalar nada no computador.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1eIhqdkXinjz4T6v9SPO4xcNU2c2ax-Jl?usp=sharing)

---

## O que tem no notebook

| Parte | Conteúdo |
|---|---|
| 0 | Configuração: chave da API do Gemini (Google AI Studio) |
| 1 | Conversando com um LLM: tokens e instrução de sistema |
| 2 | Chatbot com memória (reenvio do histórico) e onde ele falha: data, contas, dados do usuário |
| 3 | Ferramentas (*function calling*): o modelo **pede**, o nosso código **executa** |
| 4 | O loop do agente no padrão **ReAct**: pensar → agir → observar → responder |
| 5 | Projeto **Estudaí**, com estas ferramentas:<br>• `obter_data_hora`, `dias_ate`<br>• `calcular`, com `ast` em vez de `eval`<br>• `buscar_wikipedia`<br>• lista de tarefas<br>• `planejar_pomodoros`<br>• bônus: interface web com Gradio |
| 6 | Desafios: feriados com a BrasilAPI (resolvido), cotação de moedas com a Frankfurter, um agente com foco e um agente próprio |
| 7 | Limitações e segurança: injeção de prompt, menor privilégio, humano no circuito, alucinação, custo e LGPD |

O gabarito dos desafios fica no fim do notebook.

## Como usar

1. Clique em **Abrir no Colab** e depois em **Arquivo → Salvar uma cópia no Drive**.
2. Gere uma chave em <https://aistudio.google.com/apikey>.
3. Rode as células em ordem. A chave é pedida com `getpass`, então ela não fica gravada no notebook.

> **Nunca** cole a chave da API no código, nem a publique no GitHub ou em prints. Quem tem a chave usa a sua cota.

---

## Projetos dos participantes

Dois participantes publicaram agentes que construíram a partir do minicurso.

### 1. Estudaí com acesso ao GitHub

**Repositório:** [Alguem5381/agente-curso](https://github.com/Alguem5381/agente-curso)

**Autor:** Júlio Cesar Lima de Souza

O autor partiu do notebook do minicurso e deu ao Estudaí **três ferramentas novas** que usam a API REST pública do GitHub:

| Ferramenta | O que faz |
|---|---|
| `get_github_repository_root` | lista os arquivos da raiz de um repositório |
| `search_in_github_repository_path` | lista o conteúdo de uma pasta (ex.: `/src`) |
| `download_github_file` | baixa o conteúdo de um arquivo |

Com elas, o agente consegue explicar um projeto de código a partir dos próprios arquivos do repositório.

No exemplo do notebook, o agente recebe o pedido para explicar a biblioteca *FlowOnRails* (C#), do mesmo autor. Ele então:

1. chama `get_github_repository_root`;
2. baixa o `README.md`;
3. discute a estrutura e as decisões de implementação.

Esse projeto mostra o que a Parte 7 discute: uma ferramenta que traz texto de fora para o contexto do agente. Por isso é um bom caso para testar injeção de prompt.

**Como rodar:** abra o notebook `Cópia_de_Agente_IA_Python_Minicurso.ipynb` no Colab e siga as mesmas instruções do material.

### 2. Agente de conversão de moedas

**Repositório:** [XInel-s/cambio-frankfurter-ai-agent](https://github.com/XInel-s/cambio-frankfurter-ai-agent)

Este projeto parte do **Desafio 1** (cotação de moedas) e o leva para fora do Colab. É um script Python de terminal (`Conversor.py`) que responde a perguntas de câmbio em linguagem natural.

Ele usa uma única ferramenta, `consult_cotacao(orig_coin, dest_coin, val)`:

- consulta a taxa atual na API [Frankfurter](https://frankfurter.dev/);
- converte o valor entre **duas moedas quaisquer**, não só para reais;
- devolve o resultado com a data da cotação.

Detalhes do script:

- usa `client.chats.create`, com o loop automático de *function calling* do SDK e `temperature=0.0`;
- lê a chave da variável de ambiente `GEMINI_API_KEY`, em vez de deixá-la no código.

**Como rodar:**

```bash
pip install google-genai requests
export GEMINI_API_KEY="sua_chave_aqui"   # no fish: set -x GEMINI_API_KEY "sua_chave_aqui"
python3 Conversor.py
```

---

## Para ir além

- **Frameworks de agentes:** Google ADK, LangGraph, CrewAI, OpenAI Agents SDK.
- **MCP (Model Context Protocol):** padrão aberto para conectar ferramentas a qualquer agente.
- **RAG:** dar ao agente acesso aos *seus* documentos, como os PDFs de uma disciplina.

## Referências

1. GOOGLE. *Gemini API: Getting Started*. <https://ai.google.dev/gemini-api/docs/get-started>
2. GOOGLE. *Function Calling with the Gemini API*. <https://ai.google.dev/gemini-api/docs/function-calling>
3. GOOGLE. *Google Colaboratory*. <https://colab.research.google.com/>
4. PYTHON SOFTWARE FOUNDATION. *The Python Tutorial*. <https://docs.python.org/3/tutorial/>
5. YAO, S. et al. *ReAct: Synergizing Reasoning and Acting in Language Models*. ICLR, 2023. <https://arxiv.org/abs/2210.03629>
