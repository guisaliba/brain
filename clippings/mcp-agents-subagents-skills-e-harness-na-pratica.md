---
tags:
  - clippings
description:
created: 2024-06-09
published: 2026-06-06
author: DennisRojas
source: https://www.linkedin.com/pulse/mcp-agents-subagents-skills-e-harness-na-pr%C3%A1tica-uma-plataforma-istvf/
title: "MCP, Agents, Subagents, Skills e Harness na prática: construindo uma plataforma agentic para uma Fintech POS"
---
Quando falamos de agentes de IA para engenharia de software, muita gente mistura conceitos como MCP, Agents, Subagents, Skills, Claude Code, Codex e Harness.

Na prática, para uma fintech POS, a separação mais útil é esta:

```
Agent = executor principal
Subagent = especialista delegado
Skill = conhecimento reutilizável
MCP = acesso a ferramentas externas
Harness = ambiente que orquestra, testa e governa tudo 
```

### O cenário: API de Transações POS

Imagine uma fintech construindo uma API POS com os seguintes endpoints:

```
POST /transactions/authorize
POST /transactions/{transactionId}/confirm
POST /transactions/{transactionId}/void 
```

Requisitos importantes:

```
- Idempotência distribuída
- HMAC SHA-256
- X-Signature obrigatório
- X-Timestamp obrigatório
- Correlation ID obrigatório
- Estados: AUTHORIZED, CONFIRMED, VOIDED
- Timeout, retry, circuit breaker e bulkhead
- Nenhuma dependência de memória local 
```

Agora imagine que queremos um agente capaz de revisar PRs desse projeto.

### Onde entra cada peça?

![Conteúdo do artigo](https://media.licdn.com/dms/image/v2/D4D12AQEUOAnlj-0LWA/article-inline_image-shrink_1500_2232/B4DZ6f9J60H4AQ-/0/1780800069557?e=1782345600&v=beta&t=JzgEojJ5rFIHfs-BsPRGxfNAfx2ryW1aLiCuADYkWpw)

### Agent

O Agent principal coordena a tarefa.

Ele entende o objetivo geral:

```
"Revise este PR da API POS e diga se ele atende aos requisitos técnicos e de negócio." 
```

Ele não precisa fazer tudo sozinho. Ele pode delegar partes para subagents.

### Subagents

Subagents são agentes menores, especializados em uma parte do problema.

Exemplo:

```
Security Subagent:
- valida HMAC
- valida X-Signature
- valida X-Timestamp
- procura exposição de dados sensíveis

Idempotency Subagent:
- valida idempotência distribuída
- procura uso indevido de memória local
- valida chave terminalId + nsu

State Machine Subagent:
- valida transições de estado
- impede confirm de transação voided
- impede void de transação confirmed, se essa for a regra

Resilience Subagent:
- valida timeout
- retry com limite
- circuit breaker
- bulkhead 
```

O Agent principal recebe os resultados dos subagents e consolida o parecer final.

### Skill

A Skill é o manual operacional do domínio POS.

Exemplo de Skill:

```
# POS Transaction Review

Sempre que revisar código da API POS:

## Segurança
- Verificar HMAC SHA-256.
- Exigir X-Signature.
- Exigir X-Timestamp.
- Recusar requests com timestamp fora da janela permitida.
- Não logar PAN, CVV, track data ou dados sensíveis.

## Idempotência
- Authorize deve ser idempotente por terminalId + nsu.
- Confirm deve ser idempotente por transactionId.
- Void deve ser idempotente por transactionId.
- Não aceitar solução baseada em memória local.

## Máquina de estados
- AUTHORIZED pode ir para CONFIRMED.
- AUTHORIZED pode ir para VOIDED.
- CONFIRMED não deve voltar para AUTHORIZED.
- VOIDED não deve voltar para AUTHORIZED.

## Resiliência
- Chamadas externas devem ter timeout.
- Retry deve ser limitado e com backoff.
- Circuit breaker deve proteger dependências externas.
- Bulkhead deve isolar recursos críticos. 
```

### MCP

MCP é o acesso às ferramentas.

Ele permite que o Agent ou os Subagents consultem:

```
- GitHub
- Jira
- Confluence
- Datadog
- OpenTelemetry
- Banco de dados
- Logs
- Pipelines de CI 
```

MCP não é o agente. MCP é o adaptador.

### Harness

O Harness é a plataforma que roda tudo.

Ele decide:

```
- Qual agent usar: Codex, Claude, GPT etc.
- Quais subagents ativar.
- Quais MCP servers disponibilizar.
- Quais Skills carregar.
- Quais cenários executar.
- Como avaliar o resultado.
- Como registrar logs, métricas e auditoria. 
```

Em outras palavras:

```
Codex não é o Harness.
Claude Code não é o Harness.

Codex e Claude Code são agents.
O Harness é a camada que executa, controla e avalia esses agents. 
```

### Estrutura prática de projeto

```
pos-agent-harness/
├── agents/
│   ├── main-agent.ts
│   └── subagents/
│       ├── security-subagent.ts
│       ├── idempotency-subagent.ts
│       ├── state-machine-subagent.ts
│       └── resilience-subagent.ts
├── skills/
│   └── pos-review-skill.md
├── mcp/
│   ├── github-mcp.json
│   ├── jira-mcp.json
│   └── observability-mcp.json
├── scenarios/
│   ├── authorize-valid.json
│   ├── authorize-missing-hmac.json
│   ├── confirm-idempotent.json
│   └── void-invalid-transition.json
├── evaluations/
│   └── pos-review-evaluator.ts
└── run-harness.ts 
```

### Exemplo de cenário

```json
{
  "name": "authorize endpoint must validate security and idempotency",
  "task": "Review the authorize endpoint implementation",
  "pullRequest": {
    "repository": "fintech/pos-transactions-api",
    "number": 128
  },
  "expectedFindings": [
    "validates HMAC SHA-256",
    "requires X-Signature",
    "requires X-Timestamp",
    "requires X-Correlation-ID",
    "uses distributed idempotency",
    "does not use local memory for transaction state"
  ],
  "subagents": [
    "security",
    "idempotency",
    "state-machine",
    "resilience"
  ]
} 
```

### Exemplo de contrato dos subagents

```ts
export type ReviewFinding = {
  severity: "BLOCKER" | "MAJOR" | "MINOR" | "INFO";
  category: "SECURITY" | "IDEMPOTENCY" | "STATE_MACHINE" | "RESILIENCE";
  message: string;
  file?: string;
  line?: number;
};

export type SubagentResult = {
  name: string;
  findings: ReviewFinding[];
  summary: string;
};

export interface Subagent {
  name: string;
  review(input: ReviewInput): Promise<SubagentResult>;
}

export type ReviewInput = {
  task: string;
  repository: string;
  pullRequestNumber: number;
  files: RepositoryFile[];
  skill: string;
};

export type RepositoryFile = {
  path: string;
  content: string;
}; 
```

### Exemplo de Security Subagent

```ts
import { ReviewInput, SubagentResult } from "./types";

export class SecuritySubagent {
  name = "security";

  async review(input: ReviewInput): Promise<SubagentResult> {
    const findings = [];

    const allContent = input.files
      .map(file => `${file.path}\n${file.content}`)
      .join("\n\n");

    if (!allContent.includes("X-Signature")) {
      findings.push({
        severity: "BLOCKER",
        category: "SECURITY",
        message: "Authorize endpoint does not validate X-Signature header."
      });
    }

    if (!allContent.includes("X-Timestamp")) {
      findings.push({
        severity: "BLOCKER",
        category: "SECURITY",
        message: "Authorize endpoint does not validate X-Timestamp header."
      });
    }

    if (!allContent.includes("sha256") && !allContent.includes("SHA-256")) {
      findings.push({
        severity: "BLOCKER",
        category: "SECURITY",
        message: "HMAC SHA-256 validation was not found."
      });
    }

    if (allContent.includes("cvv") && allContent.includes("log")) {
      findings.push({
        severity: "MAJOR",
        category: "SECURITY",
        message: "Potential sensitive data logging detected."
      });
    }

    return {
      name: this.name,
      findings,
      summary: findings.length === 0
        ? "Security checks passed."
        : "Security issues were found."
    };
  }
} 
```

### Exemplo de Idempotency Subagent

```ts
import { ReviewInput, SubagentResult } from "./types";

export class IdempotencySubagent {
  name = "idempotency";

  async review(input: ReviewInput): Promise<SubagentResult> {
    const findings = [];

    const allContent = input.files
      .map(file => file.content)
      .join("\n\n");

    const hasTerminalId = allContent.includes("terminalId");
    const hasNsu = allContent.includes("nsu");
    const hasDistributedStore =
      allContent.includes("redis") ||
      allContent.includes("dynamodb") ||
      allContent.includes("postgres") ||
      allContent.includes("cassandra");

    const usesLocalMemory =
      allContent.includes("Map<") ||
      allContent.includes("ConcurrentHashMap") ||
      allContent.includes("globalThis") ||
      allContent.includes("static map");

    if (!hasTerminalId || !hasNsu) {
      findings.push({
        severity: "BLOCKER",
        category: "IDEMPOTENCY",
        message: "Authorize idempotency must use terminalId + nsu."
      });
    }

    if (!hasDistributedStore) {
      findings.push({
        severity: "BLOCKER",
        category: "IDEMPOTENCY",
        message: "Distributed idempotency store was not found."
      });
    }

    if (usesLocalMemory) {
      findings.push({
        severity: "BLOCKER",
        category: "IDEMPOTENCY",
        message: "Local memory must not be used for idempotency or transaction state."
      });
    }

    return {
      name: this.name,
      findings,
      summary: findings.length === 0
        ? "Idempotency checks passed."
        : "Idempotency issues were found."
    };
  }
} 
```

### Exemplo de State Machine Subagent

```ts
import { ReviewInput, SubagentResult } from "./types";

export class StateMachineSubagent {
  name = "state-machine";

  async review(input: ReviewInput): Promise<SubagentResult> {
    const findings = [];

    const allContent = input.files
      .map(file => file.content)
      .join("\n\n");

    const hasAuthorized = allContent.includes("AUTHORIZED");
    const hasConfirmed = allContent.includes("CONFIRMED");
    const hasVoided = allContent.includes("VOIDED");

    if (!hasAuthorized || !hasConfirmed || !hasVoided) {
      findings.push({
        severity: "BLOCKER",
        category: "STATE_MACHINE",
        message: "Transaction state machine must support AUTHORIZED, CONFIRMED and VOIDED states."
      });
    }

    if (!allContent.includes("AUTHORIZED") || !allContent.includes("CONFIRMED")) {
      findings.push({
        severity: "MAJOR",
        category: "STATE_MACHINE",
        message: "Could not verify transition from AUTHORIZED to CONFIRMED."
      });
    }

    if (!allContent.includes("AUTHORIZED") || !allContent.includes("VOIDED")) {
      findings.push({
        severity: "MAJOR",
        category: "STATE_MACHINE",
        message: "Could not verify transition from AUTHORIZED to VOIDED."
      });
    }

    return {
      name: this.name,
      findings,
      summary: findings.length === 0
        ? "State machine checks passed."
        : "State machine issues were found."
    };
  }
} 
```

### Exemplo do Main Agent

```ts
import { SecuritySubagent } from "./subagents/security-subagent";
import { IdempotencySubagent } from "./subagents/idempotency-subagent";
import { StateMachineSubagent } from "./subagents/state-machine-subagent";
import { ResilienceSubagent } from "./subagents/resilience-subagent";
import { ReviewInput, ReviewFinding } from "./types";

export class PosReviewAgent {
  private subagents = [
    new SecuritySubagent(),
    new IdempotencySubagent(),
    new StateMachineSubagent(),
    new ResilienceSubagent()
  ];

  async review(input: ReviewInput) {
    const results = [];

    for (const subagent of this.subagents) {
      const result = await subagent.review(input);
      results.push(result);
    }

    const findings: ReviewFinding[] = results.flatMap(result => result.findings);

    return {
      approved: !findings.some(finding => finding.severity === "BLOCKER"),
      findings,
      subagentResults: results,
      summary: this.buildSummary(findings)
    };
  }

  private buildSummary(findings: ReviewFinding[]) {
    const blockers = findings.filter(f => f.severity === "BLOCKER");

    if (blockers.length > 0) {
      return `PR blocked. ${blockers.length} blocker issue(s) found.`;
    }

    return "PR approved by POS review agent.";
  }
} 
```

### Exemplo do Harness

```ts
import fs from "node:fs/promises";
import path from "node:path";
import { PosReviewAgent } from "./agents/main-agent";
import { fetchPullRequestFiles } from "./mcp/github-client";
import { evaluateResult } from "./evaluations/pos-review-evaluator";

type Scenario = {
  name: string;
  task: string;
  pullRequest: {
    repository: string;
    number: number;
  };
  expectedFindings: string[];
  subagents: string[];
};

async function runHarness() {
  const scenarioPath = path.join(
    process.cwd(),
    "scenarios",
    "authorize-missing-hmac.json"
  );

  const scenario: Scenario = JSON.parse(
    await fs.readFile(scenarioPath, "utf-8")
  );

  const skill = await fs.readFile(
    path.join(process.cwd(), "skills", "pos-review-skill.md"),
    "utf-8"
  );

  const files = await fetchPullRequestFiles({
    repository: scenario.pullRequest.repository,
    pullRequestNumber: scenario.pullRequest.number
  });

  const agent = new PosReviewAgent();

  const result = await agent.review({
    task: scenario.task,
    repository: scenario.pullRequest.repository,
    pullRequestNumber: scenario.pullRequest.number,
    files,
    skill
  });

  const evaluation = evaluateResult({
    result,
    expectedFindings: scenario.expectedFindings
  });

  console.log(JSON.stringify({
    scenario: scenario.name,
    approved: result.approved,
    findings: result.findings,
    evaluation
  }, null, 2));

  if (!evaluation.passed) {
    process.exit(1);
  }
}

runHarness().catch(error => {
  console.error(error);
  process.exit(1);
}); 
```

### Exemplo de avaliação

```ts
type AgentResult = {
  approved: boolean;
  findings: {
    severity: string;
    category: string;
    message: string;
  }[];
};

export function evaluateResult(input: {
  result: AgentResult;
  expectedFindings: string[];
}) {
  const outputText = input.result.findings
    .map(finding => finding.message)
    .join("\n")
    .toLowerCase();

  const missing = input.expectedFindings.filter(expected => {
    return !outputText.includes(expected.toLowerCase());
  });

  return {
    passed: missing.length === 0,
    missing,
    totalExpected: input.expectedFindings.length,
    totalMatched: input.expectedFindings.length - missing.length
  };
} 
```

### Onde Codex e Claude entram?

Codex e Claude Code entram como agents de execução.

Eles podem ser usados pelo Harness como motores diferentes.

Exemplo:

```ts
export type AgentProvider = "codex" | "claude" | "gpt";

export async function runEngineeringAgent(input: {
  provider: AgentProvider;
  task: string;
  repository: string;
  pullRequestNumber: number;
}) {
  switch (input.provider) {
    case "codex":
      return runWithCodex(input);

    case "claude":
      return runWithClaudeCode(input);

    case "gpt":
      return runWithGptAgent(input);

    default:
      throw new Error("Unsupported agent provider");
  }
} 
```

O ponto importante:

```
Codex não substitui o Harness.
Claude Code não substitui o Harness.

Eles são executores dentro do Harness. 
```

O Harness permite comparar:

```
- Codex revisou melhor este PR?
- Claude encontrou mais problemas de segurança?
- GPT gerou menos falso positivo?
- Qual agent seguiu melhor a Skill POS? 
```

### Exemplo de comparação entre agents

```ts
const providers = ["codex", "claude", "gpt"] as const;

for (const provider of providers) {
  const result = await runEngineeringAgent({
    provider,
    task: scenario.task,
    repository: scenario.pullRequest.repository,
    pullRequestNumber: scenario.pullRequest.number
  });

  const evaluation = evaluateResult({
    result,
    expectedFindings: scenario.expectedFindings
  });

  console.log({
    provider,
    passed: evaluation.passed,
    matched: evaluation.totalMatched,
    missing: evaluation.missing
  });
} 
```

### Conclusão

Em uma fintech POS, usar IA para engenharia não deveria ser apenas abrir Claude Code, Codex ou Cursor e pedir para revisar um Pull Request.

Isso ajuda, mas não escala governança.

A arquitetura mais madura separa responsabilidades:

```
MCP = conecta ferramentas
Skill = define conhecimento e padrões
Agent = executa a tarefa
Subagent = especialista em uma dimensão do problema
Harness = orquestra, testa, audita e compara tudo 
```

Para uma fintech, isso é especialmente importante porque os erros não são apenas bugs.

Eles podem virar:

```
- risco financeiro
- inconsistência transacional
- falha de auditoria
- problema regulatório
- incidente de segurança
- quebra de confiança com lojistas e adquirentes 
```

O maior ativo estratégico não é escolher entre Codex ou Claude.

O maior ativo é construir um Harness capaz de usar qualquer um deles com segurança, observabilidade, testes, Skills de domínio e subagents especializados.