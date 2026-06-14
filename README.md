# Verdant Plate Supply Planner

An AI supply-planning agent built on Microsoft 365 Copilot (Copilot Studio) that
helps operations teams spot supply risks, reason through trade-offs, and decide
what to do, grounded in data, cited, and governed.

*Built for the Microsoft Agents League Contest @ AI Skills Fest, Enterprise Agents track.*
*All data and scenarios are fictional, for demonstration only.*

---

## The problem

Every week, a supply planner at a food manufacturer has to reconcile open orders,
ingredient inventory, supplier delays, perishable stock, and production capacity to
answer one question: what is going to go wrong this week, and what should I do about
it? Doing that by hand across spreadsheets is slow, and it is easy to miss where
constraints collide.

## The solution

The Verdant Plate Supply Planner is a conversational agent for a fictional plant-based
food manufacturer (frozen meals, sauces and spreads, snack bars). A planner asks it
questions in Microsoft 365 Copilot Chat, and the agent:

- finds the week's supply risks and ranks them by severity,
- diagnoses the cause of each (e.g. a delayed supplier PO) and cites the source,
- applies standard supply-chain methods (days of supply, reorder point, ABC / priority
 segmentation, lead-time) to reason quantitatively,
- quantifies the trade-offs in dollars,
- drafts a ready-to-send expedite email to a backup supplier, and
- logs the recommended action as a task in Microsoft Planner.

It advises; the human stays in control.

## How it works (architecture)

1. The planner asks a question in Microsoft 365 Copilot Chat.
2. The agent (Copilot Studio, with Work IQ enabled as the intelligence layer) reasons
 over grounded sources only.
3. Grounding: the planning dataset (orders, inventory, recipe BOM, suppliers, capacity)
 and work-context documents (a supplier delay email and planning meeting notes).
4. Reasoning: standard supply-chain planning methods.
5. Outputs: cited risk analysis and costed recommendations, plus a ready-to-send
 expedite email draft.
6. Action: a Microsoft Planner connector writes the recommended action as a task.
7. Foundation: grounded in data only, cites every source, advises rather than acts,
 web search off.

See `architecture.png` for the diagram.

## Microsoft IQ integration

This agent uses **Work IQ**, the intelligence layer behind Microsoft 365 Copilot, to
bring in work context (supplier communications and planning notes) alongside the
structured dataset. Work IQ provides context and priority signals; all numeric values
are taken only from the dataset, never invented.

## Reliability and safety

- Answers only from grounded sources; states plainly when something is not in the data.
- Cites a source for every factual claim.
- Takes every quantity, price, and date directly from the dataset, never from memory or
 a placeholder rate.
- Keeps a consistent risk-severity scheme (Critical = blocks high-priority revenue with
 no easy fix; High = serious but with a clear mitigation).
- Advisory only: it does not place orders or send messages; it recommends and tells the
 planner where to act. The one write-action (Planner task) targets a dedicated demo plan.

## Repository contents

- `VerdantPlate_Agent_Instructions_FINAL_v3.md`, the agent's instructions (its "source")
- `VerdantPlate_SupplyPlanning_Data_v2.xlsx`, the synthetic planning dataset (knowledge)
- `GreenField_Proteins_Delay_Email.docx`, work-context document (knowledge)
- `Supply_Planning_Meeting_Notes.docx`, work-context document (knowledge)
- `VerdantPlate_Expedite_Email_Sample.md`, sample agent output (the expedite email)
- `VerdantPlate_Architecture_Notes.md`, architecture description
- `architecture.png`, architecture diagram
- `VerdantPlate_Case_Study.md`, the build story and design decisions
- `VerdantPlate_Cover.png`, project cover image
- `agent-response.png`, sample agent response (the weekly risk summary)
- `planner-task.png`, the task the agent created in Microsoft Planner

## How to reproduce

1. In Copilot Studio, create a new agent and paste in the instructions.
2. Add the three knowledge files (the dataset and the two work-context documents).
3. Enable Work IQ as the intelligence layer.
4. Add the Microsoft Planner "Create a task" connector as a tool, pointed at a dedicated
 demo plan.
5. Turn web search off. Use a stable, supported model.
6. Ask the agent about the week's supply risks to see it in action.

## Demo video

A 5-minute walkthrough of the agent in action is available here: _(link to be added once the video is uploaded to YouTube or Vimeo)_.

---

*This is a no-code project built in Microsoft Copilot Studio. The repository holds the
agent's instructions, data, documentation, and supporting artifacts rather than
traditional source code.*

