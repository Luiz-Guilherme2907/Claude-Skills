# 🧠 My Claude Skills

Repositório pessoal de skills customizadas para o Claude. Skills são arquivos de instrução (`.md`) que ensinam o Claude a se comportar de forma especializada em contextos específicos — sem precisar repetir instruções a cada conversa.

---

## Como funciona

O Claude carrega skills automaticamente quando identifica que o contexto da conversa bate com a descrição de uma skill. Cada skill vive numa pasta própria dentro de `/mnt/skills/user/` e contém:

- Um frontmatter YAML com `name` e `description` (usados para o gatilho automático)
- Um corpo com as instruções detalhadas de comportamento

```
my-skills/
├── prompt-engineer/
│   └── SKILL.md
└── nowait-reasoning/
    └── SKILL.md
```

---

## Skills disponíveis

### 🎯 prompt-engineer

**O que faz:** Transforma o Claude num especialista em engenharia de prompts. Gera prompts completos, estruturados e token-eficientes para qualquer modelo de IA.

**Quando é acionada:** Sempre que você pedir para criar, melhorar ou estruturar um prompt — frases como *"me faz um prompt para..."*, *"melhora esse meu prompt"*, *"preciso de um system prompt"*, *"prompt para Midjourney"*, etc.

**Capacidades:**
- Identifica o tipo de prompt ideal (system, task, persona, chain-of-thought, imagem, few-shot)
- Aplica regras de otimização: corta palavras desnecessárias, estrutura na ordem certa, torna o formato de saída explícito
- Adapta o estilo ao modelo-alvo (Claude, GPT-4o, Gemini, Midjourney, DALL-E, Stable Diffusion)
- Faz no máximo 2 perguntas antes de gerar — se tiver contexto suficiente, gera direto

---

### ⚡ nowait-reasoning

**O que faz:** Suprime loops de auto-reflexão redundantes no raciocínio do Claude, tornando as respostas mais diretas e econômicas em tokens.

**Quando é acionada:** Quando você pede respostas mais concisas — frases como *"seja mais direto"*, *"use menos tokens"*, *"para de ficar repetindo"*, *"você está pensando demais"*, *"responda sem rodeios"*, etc.

**Capacidades:**
- Suprime tokens de hesitação desnecessários ("Hmm", "Espera", "Na verdade, deixa eu reconsiderar...")
- Mantém o raciocínio linear e progressivo, sem voltar a passos já resolvidos
- Faz uma única verificação ao final, sem loops de re-checagem
- Baseado em pesquisa que mostra redução de 27–51% no comprimento das respostas sem perda de precisão

---

## Como criar uma nova skill

1. Crie uma pasta com o nome da skill dentro do seu diretório de skills
2. Adicione um arquivo `SKILL.md` com a estrutura:

```markdown
---
name: nome-da-skill
description: >
  Descreva aqui quando o Claude deve usar esta skill.
  Seja específico sobre as frases e contextos que devem acioná-la.
---

# Instruções detalhadas

[Comportamento esperado, regras, exemplos, templates...]
```

3. A `description` é o que o Claude lê para decidir se a skill é relevante — quanto mais clara e com exemplos de frases reais, melhor o gatilho automático.

---

## Referências

- [Claude Skills — Documentação oficial](https://docs.claude.ai/skills)
- [Prompt Engineering Guide — Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
