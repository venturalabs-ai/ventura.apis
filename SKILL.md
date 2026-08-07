# Skill: ventura.apis — LOOP Skill Engine / Deterministic Replay

Skill de descoberta e integração de APIs públicas com execução
**determinística**: explore uma vez, compile a receita, replique com ~zero
tokens, regenere quando a API (ou o projeto) mudar.

## Trigger

Use quando o usuário quiser: achar uma API para um projeto, integrar uma API
pública, testar endpoints, escolher entre APIs, montar protótipo com dados
externos.

## Arquitetura Token-Efficient & Regenerative

| Fase | Descrição | Consumo |
|---|---|---|
| **Explore** | Modelo forte analisa necessidade + categorias curadas (uma vez) | Alto (único) |
| **Compile** | Gera a receita de integração em `api.json` (determinística) | Baixo |
| **Replay** | Executa: endpoint, método, headers, valida resposta | Mínimo/Zero |
| **Regenerate** | API mudou/limitou/caiu → regenere a escolha | Sob demanda |

## Receita determinística (Replay)

```text
1. PEDIDO   — "integrar API de X" | "qual API para Y"
2. RECEITA  — consulta api.json: nome, endpoint, método, headers, limite, exemplo
3. EXECUTA  — 1 chamada de teste + valida status/estrutura/resposta
4. REGISTRA — sucesso, latência, limite restante, observações
5. STOP-YIELD — limite/custo subindo ou resposta instável → sinaliza regenerar
```

## Regras de engenharia

- **Token Budget** — Explore: até 6k tokens. Replay: < 200 tokens.
- **Context Firewall** — o replay só vê a receita da API (nunca a curadoria inteira).
- **Prefix Caching** — o sistema deste arquivo fica byte-stable.
- **Skill Distillation** — integração validada vira receita permanente.
- **Regeneração** — API descontinuada ou limite atingido → volta ao Explore.

## Como compilar a receita (Explore → Compile)

```text
1. Entrevista rápida: necessidade, formato (JSON), chave disponível, limite
2. Seleciona da categoria curada a API que atende (documentação, custo, limite)
3. Compila api.json: base_url, endpoint, método, headers, exemplo de resposta
4. Valida com 1 chamada de teste e ativa o Replay
```

## Exemplo de uso

```text
Atue como ventura.apis (modo REPLAY). Minha api.json diz: "clima para meu
dashboard, endpoint /forecast, sem chave". Liste a chamada de teste, valide a
resposta e registre o resultado. Use menos de 200 tokens.
```
