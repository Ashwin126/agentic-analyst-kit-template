# Team worksheet: design an agent team

You will **design** a team of AI agents for one business question. You will not build or run it today.
Read the [data card](DATA_CARD.md) first.

## The rules

- **3 to 5 agents**, plus **1 reviewer agent** (required). The reviewer did not do the work and checks it.
- Every arrow between agents passes a **named file** (for example `orders_joined.csv`).
- Put a **check** on your **3 most important hand-offs**.
- Add at least **one human stop**: a point where a person must decide before the team goes on.

## Pick one question card

1. **About 15% of reviews are 1 or 2 stars. Which one fix should Olist fund:** faster delivery, cutting bad sellers, or better product listings?
2. **Which sellers should Olist cut, coach, or reward?**
3. **Should Olist promise 7-day delivery across Brazil?**
4. **Build a Monday-morning customer health report** that runs every week.
5. **Turn Portuguese customer complaints into action tickets** for the right team. Refunds need a human to approve.

## What you hand in (3 parts)

### 1. Diagram (Mermaid)
Describe your design to any AI chat and paste this:

```
Turn this agent design into a Mermaid flowchart (flowchart TD).
Use three step types and label each box with its type:
- AGENT (AI makes a judgment): dark navy box, white text.
- WORKFLOW (a fixed rule, script or tool call, no AI judgment): light blue box.
- HUMAN (a person decides): gold diamond.
Put the file each step hands over on the arrow.
Show steps that only happen sometimes as dotted arrows.
Use these classDef lines:
classDef agent fill:#0B2545,stroke:#0B2545,color:#F6F3EC
classDef workflow fill:#DCE8F7,stroke:#2F6FDB,color:#14213D
classDef human fill:#FCE9B8,stroke:#8A5A00,color:#14213D
Design: <describe your steps, files, checks and human stops>
```

View it at [mermaid.live](https://mermaid.live). Take a screenshot for your slide.

**Agent or workflow?** If the step needs judgment (reading text, choosing, writing, checking), it is an agent. If it always does the same thing (joining tables, computing a fixed metric, sending a file), it is a workflow step.

**Example:** a voice shopping assistant (not an Olist card), drawn this way. Paste it into mermaid.live to see it.

```mermaid
flowchart TD
    V(["Voice note: 2 kilo potato"]) --> L["AGENT · Listener: understands the request"]
    L -- "order.json" --> H1{"HUMAN · Read back: 2 kg potatoes? She confirms"}
    H1 --> S["AGENT · Shopper: picks items, fills cart"]
    S -- "cart.json" --> C["AGENT · Checker (reviewer): cart matches order? under limit?"]
    C -- "OK" --> O["WORKFLOW · Place order: tool call, voice update"]
    C -. "over limit or substitute" .-> H2{"HUMAN · Her son approves"}
    H2 --> O
    classDef agent fill:#0B2545,stroke:#0B2545,color:#F6F3EC
    classDef workflow fill:#DCE8F7,stroke:#2F6FDB,color:#14213D
    classDef human fill:#FCE9B8,stroke:#8A5A00,color:#14213D
    class L,S,C agent
    class O workflow
    class H1,H2 human
```

### 2. Agent prompts (2 lines each)
For every agent, including the reviewer:

| Agent | Line 1: your job | Line 2: your limits |
| --- | --- | --- |
| Example: Data agent | Join orders, payments, reviews and customers into one row per order. | Never change the raw files. Stop and ask if more than 2% of orders fail to join. |
| | | |

### 3. One-page defense
Answer each in 1 or 2 lines:

1. **Roles:** what does each agent do, and why is it a separate agent?
2. **Checks:** what is checked at your 3 most important hand-offs, and how?
3. **Human stop:** where must a person decide, and why there?
4. **Reviewer:** what does your reviewer check that the other agents cannot check themselves?
5. **Cut:** one agent you chose **not** to add, and why.
6. **Trade-offs:** 2 advantages and 2 risks of your design.

## What makes a good design

| Test | Good sign | Warning sign |
| --- | --- | --- |
| **Every agent earns its place** | You can say what breaks if you remove it | Two agents do almost the same job |
| **One clear job each** | Each job fits in one sentence | An agent "does the analysis" |
| **Concrete hand-offs** | Each arrow passes a named file | Arrows say "sends info" |
| **Real checks** | A check someone could run: row counts, join rate, read 20 samples | "The AI double-checks" |
| **Independent review** | The reviewer did not do the work | Agents only check their own work |
| **Humans where it matters** | A person decides before money, people or customers are affected | No human stop, or a stop at every step |
| **Answers the question** | Ends in a decision or a report someone will use | Ends in "insights" |

Start simple. Anthropic's advice for agent systems: use the simplest design that works, and add agents only when the task needs them.
Source: [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents).
