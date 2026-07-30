Here are your **simple, clean notes** 👇 (easy to revise before interview 🚀)

---

# 🛡️ Guardrails in Multi-Agent System (Simple Notes)

## 🔹 What are Guardrails?

- Safety checks for **input and output**
- Help prevent:
    - malicious requests
    - wrong responses
    - unnecessary cost (expensive models)

👉 Think: **middleware for validation**

---

# 🧩 Types of Guardrails

## 1️⃣ Input Guardrails

- Run on **user input**
- Execute **before agent starts**

### ✔️ Use cases:

- Block harmful queries
- Validate format (email, JSON, etc.)

### ⚙️ Flow:

1. Receive input
2. Run validation
3. If ❌ → **Tripwire triggers (stop execution)**

---

## 2️⃣ Output Guardrails

- Run on **final response**

### ✔️ Use cases:

- Remove sensitive data
- Ensure correct format

### ⚙️ Flow:

1. Agent produces output
2. Guardrail checks it
3. If ❌ → **Tripwire triggers**

---

## 3️⃣ Tool Guardrails

- Run on **every tool (function call)**

### ✔️ Use cases:

- Validate API inputs
- Sanitize DB queries

### ⚙️ Runs:

- Before tool execution (input check)
- After tool execution (output check)

---

# 🚨 Tripwire (Important)

- If something is wrong → **tripwire = true**
- System:
    - ❌ stops execution immediately
    - throws error

👉 Think: **circuit breaker**

---

# 🔄 Workflow Rules (Very Important)

- Input guardrails → only **first agent**
- Output guardrails → only **last agent**
- Tool guardrails → **every tool call**

---

# ⚡ Execution Modes

## 🟢 runInParallel = true (default)

- Runs guardrail + model together
- Faster ⚡
- But may waste tokens 💸

## 🔴 runInParallel = false

- Runs guardrail first
- Safer + cheaper
- Slightly slower

---

# 🧠 Simple Example (Your Backend Thinking)

### Scenario:

User sends:

```json
{ "title": "<script>alert('hack')</script>" }
```

### Flow:

👉 Input Guardrail

- Detects script injection ❌
- Tripwire triggers → request blocked

👉 Model never runs → saves cost

---

# 💡 Key Insight

- Guardrails = **security + cost optimization**
- Handoffs = **control flow between agents**

👉 Together they build:

**Production-level AI systems**

---

# 🚀 Pro Tip (for you)

When you build AI + backend system:

- Use guardrails like:
    
    - `Joi / Zod` → input validation
    - middleware → security
- Think of guardrails as:
    
    👉 “AI middleware layer”
    

---

# 7. Input Guardrails

```jsx
import 'dotenv/config';
import { Agent, run, InputGuardrailTripwireTriggered } from '@openai/agents';
import { z } from 'zod';

const mathInputAgent = new Agent({
  name: 'Math query checker',
  instructions: `
  You are an input guardrail agent that checks if the user query is a maths question or not
  Rules:
  - The question has to be strictyly a maths equation only.
  - Reject any other kind of request ven if related to maths.
  `,
  outputType: z.object({
    isValidMathsQuestion: z.boolean().describe('if the question is a maths q'),
    reason: z.string().optional().describe('reason to reject'),
  }),
});

const mathInputGuardrail = {
  name: 'Math Homework Guardrail',
  execute: async ({ input }) => {
    const result = await run(mathInputAgent, input);
    return {
      outputInfo: result.finalOutput.reason,
      tripwireTriggered: !result.finalOutput.isValidMathsQuestion, // <-- This value decides if we have to trigger
    };
  },
};

const mathsAgent = new Agent({
  name: 'Maths Agent',
  instructions: 'You are an expert maths ai agent',
  inputGuardrails: [mathInputGuardrail],
});

async function main(q = '') {
  try {
    const result = await run(mathsAgent, q);
    console.log(`Result`, result.finalOutput);
  } catch (e) {
    if (e instanceof InputGuardrailTripwireTriggered) {
      console.log(`Invalid Input: Rejected because ${e.message}`);
    }
  }
}

main('2 +2 = ?');
```

# 8. Output Guardrails

Output guardrails run in 3 steps:

1. The guardrail receives the output produced by the agent.
2. The guardrail function executes and returns a [`GuardrailFunctionOutput`](https://openai.github.io/openai-agents-js/openai/agents/interfaces/guardrailfunctionoutput) wrapped inside an [`OutputGuardrailResult`](https://openai.github.io/openai-agents-js/openai/agents/interfaces/outputguardrailresult).
3. If `tripwireTriggered` is `true`, an [`OutputGuardrailTripwireTriggered`](https://openai.github.io/openai-agents-js/openai/agents/classes/outputguardrailtripwiretriggered) error is thrown.

> **Note** Output guardrails only run if the agent is the _last_ agent in the workflow. For realtime voice interactions see [the voice agents guide](https://openai.github.io/openai-agents-js/guides/voice-agents/build#guardrails).

Output guardrail functions also receive an optional `details` object with the underlying `modelResponse` and the generated output items for the turn. Use this when the final output alone is not enough to decide whether the response should pass, for example when you want to inspect the full generated item list or provider response metadata before tripping the guardrail.