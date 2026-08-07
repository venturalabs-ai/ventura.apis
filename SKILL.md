# Skill: ventura.apis — LOOP Skill Engine / Constrained Replay

![License](https://img.shields.io/github/license/venturalabs-ai/ventura.apis)
![Stars](https://img.shields.io/github/stars/venturalabs-ai/ventura.apis)

Skill de descoberta e integração de APIs públicas com **replay restrito por receita**: explore quando necessário, registre a decisão, reutilize o contrato e regenere quando a API ou o projeto mudar.

## Trigger

Use quando o usuário quiser encontrar, comparar, testar ou integrar uma API pública.

## Arquitetura de eficiência

| Fase | Descrição | Meta de contexto |
|---|---|---|
| **Explore** | Analisa necessidade e opções disponíveis | Maior |
| **Compile** | Registra a integração em `api.json` | Reduzida |
| **Constrained Replay** | Reutiliza endpoint, método, headers e validação já registrados | Mínima necessária |
| **Regenerate** | Reavalia quando contrato, custo ou disponibilidade mudar | Sob demanda |

O consumo real de tokens depende do modelo, runtime, prompt e ferramentas. Este projeto não afirma execução com zero tokens nem determinismo de saídas LLM.

## Receita de replay

```text
1. PEDIDO   — necessidade de integração
2. RECEITA  — consulta api.json: nome, endpoint, método, headers, limite, exemplo
3. EXECUTA  — chamada de teste + valida status/estrutura/resposta
4. REGISTRA — sucesso, latência, limite restante, observações
5. STOP-YIELD — custo, erro ou instabilidade → sinaliza regenerar
```

## Regras de engenharia

- **Token Budget** — definir limite mensurável por runtime; não assumir valor universal.
- **Context Firewall** — replay usa somente o contexto necessário à integração.
- **Stable Prefix** — manter instruções estáveis quando o provedor oferecer cache compatível.
- **Skill Distillation** — integração validada vira receita versionada.
- **Regeneração** — API descontinuada, contrato alterado ou limite atingido → volta ao Explore.

## Compilar uma receita

```text
1. Defina necessidade, formato, autenticação e limites.
2. Selecione uma API e confirme documentação/termos atuais.
3. Registre api.json: base_url, endpoint, método, headers e contrato esperado.
4. Faça uma chamada de teste e registre o resultado.
```

## Exemplo

```text
Atue como ventura.apis em modo CONSTRAINED REPLAY. Use a receita api.json,
execute a validação necessária e registre o resultado sem reabrir decisões já documentadas.
```
