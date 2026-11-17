# Do Chatbot ao Agente: criando seu primeiro agente de IA com Python

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SEU-USUARIO/do-chatbot-ao-agente/blob/main/notebook/Agente_IA_Python_Minicurso.ipynb)

Material do minicurso ministrado por Mariana em 10 de novembro de 2026. Em quatro horas, os participantes saíram de uma simples pergunta a um modelo de linguagem até um **agente de IA** que consulta a Wikipédia, faz contas com precisão, sabe que dia é hoje e organiza tarefas de estudo, tudo em Python, no Google Colab, com a API do Gemini.

A ideia central do minicurso cabe numa frase: **o modelo não executa nada, ele pede; quem executa é o nosso código.** Um agente é um LLM que decide quais ferramentas usar, em um loop, até concluir a tarefa.

## O que você vai aprender

- O que é um modelo de linguagem (LLM) e por que, sozinho, ele não sabe a data, não consulta nada e erra contas
- A diferença entre um chatbot de regras, um chatbot com LLM e um agente de IA
- Como integrar um LLM a um programa Python por meio de uma API
- Como transformar funções Python em ferramentas (*function calling*)
- Como escrever, à mão, o loop de um agente no padrão ReAct (pensar → agir → observar)
- As limitações e os riscos dos agentes, como alucinação e injeção de prompt

## Como usar

**No Google Colab (recomendado, não precisa instalar nada):**

1. Clique no botão **Abrir no Colab**, no topo desta página.
2. Gere uma chave gratuita da API do Gemini em [aistudio.google.com/apikey](https://aistudio.google.com/apikey).
3. Rode as células em ordem com `Shift + Enter`. Quando a célula de configuração pedir, cole a sua chave.

**No seu computador:**

```bash
git clone https://github.com/SEU-USUARIO/do-chatbot-ao-agente.git
cd do-chatbot-ao-agente
pip install -r requirements.txt
jupyter notebook notebook/Agente_IA_Python_Minicurso.ipynb
```

> **Cuidado com a chave da API.** Ela funciona como uma senha: quem tem a chave gasta a sua cota. O notebook pede a chave na hora e não a salva. Nunca coloque a chave no código nem a envie para o GitHub.

**Pré-requisitos:** lógica de programação e noções de Python (variáveis, funções e condicionais). Não é preciso saber nada de IA.

## Conteúdo do notebook

| Parte | O que se constrói |
|---|---|
| 0 | Configuração da chave da API |
| 1 | Primeira chamada a um LLM, tokens e instrução de sistema |
| 2 | Um chatbot com memória, e onde ele falha |
| 3 | A primeira ferramenta: o modelo pede, o nosso código executa |
| 4 | O loop do agente (padrão ReAct) |
| 5 | Projeto: **Estudaí**, o agente assistente de estudos |
| 6 | Desafios de personalização |
| 7 | Injeção de prompt, limitações e segurança |

### O agente Estudaí

O projeto final é um assistente de estudos com oito ferramentas. Cada uma resolve uma limitação que o chatbot mostrou na Parte 2.

| Ferramenta | O que faz |
|---|---|
| `obter_data_hora`, `dias_ate` | Sabe que dia é hoje e quantos dias faltam para uma prova |
| `calcular` | Faz contas com precisão (com `ast`, sem `eval`) |
| `buscar_wikipedia` | Consulta a Wikipédia em português e cita o link |
| `adicionar_tarefa`, `listar_tarefas`, `concluir_tarefa` | Organiza as tarefas de estudo |
| `planejar_pomodoros` | Monta um cronograma com a técnica Pomodoro |

Exemplo de pergunta em que o agente encadeia ferramentas sozinho: *“Tenho 1h30 livre. Monta um plano de pomodoros com as minhas tarefas pendentes.”* Ele chama `listar_tarefas`, lê o resultado e só então chama `planejar_pomodoros`.

## Resultados dos alunos

Durante os desafios, os participantes criaram os próprios agentes. Os códigos estão na pasta [`resultados-alunos/`](resultados-alunos/).

| Agente | Autor(a) | O que faz |
|---|---|---|
| [Agente 1](resultados-alunos/agente-1/) | [nome do aluno] | [descrição em uma frase] |
| [Agente 2](resultados-alunos/agente-2/) | [nome do aluno] | [descrição em uma frase] |

## Estrutura do repositório

```
do-chatbot-ao-agente/
├── notebook/
│   └── Agente_IA_Python_Minicurso.ipynb   # todo o conteúdo prático
├── slides/                                # slides do minicurso (PDF)
├── resultados-alunos/                     # agentes criados pelos participantes
├── requirements.txt
├── LICENSE
└── README.md
```

## Tecnologias

- Python 3.10+
- [Google Gen AI SDK](https://pypi.org/project/google-genai/) (`google-genai`) e o modelo `gemini-3.5-flash-lite`
- Google Colab
- APIs públicas: Wikipédia, [BrasilAPI](https://brasilapi.com.br) e [Frankfurter](https://frankfurter.dev)
- [Gradio](https://www.gradio.app), para a interface web opcional

## Referências

1. GOOGLE. *Gemini API: Getting Started*. Disponível em: https://ai.google.dev/gemini-api/docs/get-started
2. GOOGLE. *Function Calling with the Gemini API*. Disponível em: https://ai.google.dev/gemini-api/docs/function-calling
3. GOOGLE. *Google Colaboratory*. Disponível em: https://colab.research.google.com/
4. PYTHON SOFTWARE FOUNDATION. *The Python Tutorial*. Disponível em: https://docs.python.org/3/tutorial/
5. YAO, S. et al. *ReAct: Synergizing Reasoning and Acting in Language Models*. ICLR, 2023. Disponível em: https://arxiv.org/abs/2210.03629

## Licença

O material do minicurso está sob a licença MIT (veja [LICENSE](LICENSE)). Os códigos em `resultados-alunos/` pertencem aos respectivos autores e foram publicados com a autorização deles.
