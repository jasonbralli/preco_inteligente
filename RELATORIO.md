# RELATÓRIO TÉCNICO · PRE-O INTELIGENTE

## Pontos Positivos

| Item | Detalhe |
|------|---------|
| **Stack limpa** | HTML/CSS/JS puro, sem dependências, carrega instantaneamente |
| **Acessibilidade** | Skip link, ARIA labels, contraste WCAG (#5c3d1e/#c8a96e), navegação por teclado |
| **UX intuitiva** | Sliders + inputs sincronizados, tooltips explicativos, manual expansível |
| **Responsividade** | Grid adaptável, funciona em mobile |
| **Feedback visual** | Cores semânticas (verde/amarelo/laranja/vermelho) para margem de lucro |
| **Cálculo em tempo real** | Sem botão "calcular", atualiza automaticamente |
| **Documentação** | README completo com fórmulas, exemplos e instruções de deploy |
| **Validação robusta** | `sanitizeInput()` + `validateInput()` com feedback visual (borda vermelha + mensagem) |
| **Tooltips mobile** | Funcionam via `tabindex="0"` e `:focus`, não dependem de hover |
| **Testes unitários** | Suite HTML com 20+ testes para `sanitizeInput`, `validateInput`, `clamp`, `profitColor` |

---

## Pontos Negativos / Áreas de Atenção

| Item | Detalhe |
|------|---------|
| **Limites hardcoded** | `max: 999` e `max: 9999` podem ser insuficientes para pousadas premium |
| **Tooltips em mobile** | Funcionam via focus, mas ainda podem ser intrusivos em telas pequenas |

---

## Explicação: Validação de Entrada

A validação de entrada garante que os dados digitados pelo usuário estão corretos, dentro dos limites esperados e não quebram a aplicação.

### Implementação Atual

```javascript
// Remove R$, espaços, vírgulas e pontos de milhar
function sanitizeInput(str) {
  if (str === null || str === undefined) return "";
  return String(str).replace(/[R$\s.]/g, '').replace(',', '.').trim();
}

// Validação robusta com retorno detalhado
function validateInput(raw, min, max) {
  const sanitized = sanitizeInput(raw);
  if (sanitized === "" || sanitized === "-") {
    return { valid: false, value: min, error: "Campo vazio" };
  }
  const n = parseFloat(sanitized);
  if (isNaN(n)) return { valid: false, value: min, error: "Valor inválido" };
  if (n < min) return { valid: false, value: min, error: "Ajustado para mínimo" };
  if (n > max) return { valid: false, value: max, error: "Ajustado para máximo" };
  return { valid: true, value: n, error: null };
}
```

**Funciona:**
- Remove símbolos de moeda e formatação brasileira (R$ 1.234,56 → 1234.56)
- Validação de tipo (rejeita texto puro como "abc")
- Limites rigorosos (min/max) com mensagem de erro específica
- Feedback visual: borda vermelha + mensagem abaixo do campo
- Tratamento de colagem (paste) — sanitiza antes de inserir no input

---

## Explicação: Testes Unitários

Testes unitários são funções automatizadas que verificam se partes individuais do código funcionam corretamente.

### Suite de testes (`test.html`)

```javascript
// sanitizeInput
assertEqual(sanitizeInput("R$ 50,00"), "50.00");
assertEqual(sanitizeInput("R$ 1.234,56"), "1234.56");

// validateInput
const r = validateInput("R$ 75,50", 0, 100);
assertTrue(r.valid && r.value === 75.5);

// clamp
assertEqual(clamp(-10, 0, 100), 0);
assertEqual(clamp(150, 0, 100), 100);

// profitColor
assertEqual(profitColor(50), '#22c55e');  // verde
assertEqual(profitColor(40), '#eab308');  // amarelo
assertEqual(profitColor(-5), '#ef4444');  // vermelho
```

**Como executar:** Abra `test.html` no navegador — não requer servidor.

---

## Itens Concluídos (30/06/2026)

| Item | Status |
|------|--------|
| **Validação robusta de entrada** | ✅ Implementado (`sanitizeInput`, `validateInput`) |
| **Testes unitários** | ✅ Implementado (`test.html` com 20+ testes) |
| **Tooltips acessíveis em mobile** | ✅ Implementado (`tabindex="0"` + `:focus`) |
| **Tratamento de erros visual** | ✅ Implementado (`.input-error` border-red) |
| **Feedback visual de erro (borda vermelha)** | ✅ Implementado (`.param-error` + `role="alert"`) |

---

## Itens em Aberto

| # | Item | Prioridade | Status |
|---|------|------------|--------|
| 1 | **Limites de entrada configuráveis** | 🟡 Baixa | ❌ Não iniciado |
| 2 | **Modo escuro** | 🟢 Futuro | ❌ Backlog |

---

### Itens Descartados (conforme orientação)

| Item | Motivo |
|------|--------|
| **Persistência (localStorage)** | Usuário quer apenas uma calculadora volátil |
| **Exportação CSV** | Usuário não precisa de relatórios no momento |
| **Multiplicador de temporada** | Usuário argumentou que margem de lucro já compensa sazonalidade |

---

## Como Testar as Novas Funcionalidades

1. **Validação robusta:** Digite valores negativos, cole "R$ 50,00" ou texto inválido
2. **Feedback visual:** Observe a borda vermelha e mensagem de erro abaixo do campo
3. **Tooltips mobile:** Toque no ícone "?" (funciona via focus, não hover)
4. **Testes unitários:** Abra `test.html` no navegador

---

*Última atualização: 30/06/2026*