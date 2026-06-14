# Verdant Plate Supply Planner: Case Study

*An AI supply-planning agent built on Microsoft 365 Copilot, for operations teams.*
*All data and scenarios are fictional, for demonstration only.*

## Summary

The Verdant Plate Supply Planner is a conversational AI agent that helps a supply
planner at a plant-based food manufacturer answer the question they face every week:
what is going to go wrong, and what should I do about it? It reads the planning data,
reasons through the week's risks using standard supply-chain methods, quantifies the
trade-offs in dollars, and turns its analysis into action, a drafted supplier email and
a logged task, while citing every source and leaving the decision to the human.

## The problem

A supply planner has to reconcile several moving parts at once: open customer orders,
ingredient inventory, supplier deliveries (and delays), perishable stock that expires,
and finite production capacity. The hard part is not any single number, it is seeing
where these constraints collide. A delayed protein shipment, an expiring batch of cream,
and an overloaded production line are easy to track separately and easy to mishandle
together. Done by hand across spreadsheets, this is slow and error-prone.

## What the agent does

The agent works through a consistent reasoning chain: net demand from open orders,
ingredient shortfalls against inventory and inbound supply, the cause of each shortfall,
perishability, business impact ranked by order priority and value, and production
capacity. It then generates options with trade-offs and recommends one.

On top of that chain, it applies recognized supply-chain planning methods so its
reasoning reads like a practitioner's:

- Days of supply, how many days of cover remain at current demand
- Reorder point and safety stock, when stock crosses the threshold
- ABC / priority segmentation, protect high-priority, high-value orders first
- Lead-time awareness, when a shortfall actually bites, given supplier lead times

## A worked example

The demonstration data contains four interacting risks for one production week:

1. A critical pea protein shortfall, a supplier shipment slipped two weeks, leaving
 on-hand stock below safety, affecting most of the product line.
2. A batch of cashew cream expiring within days.
3. A frozen-meals production line scheduled above capacity.
4. A demand spike on the flagship lasagna.

The agent's strongest move is connecting two of these. The lasagna needs both the
delayed protein and the expiring cream, so it cannot consume the cream in time. The
alfredo sauce uses the cream but not the protein. So the agent recommends routing the
expiring cream into an alfredo run, avoiding a write-off and using spare capacity on
another line. That is the kind of cross-constraint insight a static dashboard does not
surface.

On the protein, it calculates the exact bridge quantity needed to cover only the
high-priority orders, recommends the backup supplier, and quantifies the trade-off: a
modest premium to protect several times that in at-risk revenue.

## Turning analysis into action

The agent does not stop at advice. It drafts a clean, ready-to-send expedite email to
the backup supplier with the verified quantity, and it can log the recommended action as
a task in Microsoft Planner, so the recommendation becomes something the team tracks.
It advises and prepares; the human reviews and decides.

## How it is built

The agent is built in Microsoft Copilot Studio and hosted in Microsoft 365 Copilot
Chat. It uses Work IQ as its intelligence layer, bringing in work context (a supplier
delay email and planning meeting notes) alongside a structured planning dataset. A
Microsoft Planner connector provides the write-action. No code was required, the agent
is defined by its instructions, its grounded knowledge, and its connected tools.

## Reliability and governance

Reliability was a primary design goal, not an afterthought:

- The agent answers only from grounded sources and says plainly when something is not in
 the data, rather than inventing an answer.
- Every factual claim cites its source.
- Every quantity, price, and date is taken directly from the dataset, never from memory
 or a placeholder, so the numbers in a recommendation can be trusted.
- Risk severity follows a consistent rule, so the same situation is rated the same way.
- The agent is advisory: it recommends actions and prepares drafts, but a human places
 orders and sends messages. Its one write-action targets a dedicated demonstration plan.

## What I would do next

- Connect the agent to a live data source for current visibility rather than a snapshot.
- Add forward-looking projections (e.g. estimated stock-out dates) as explicitly labeled
 forecasts.
- Extend the write-actions to additional systems through secured connectors.

## What this demonstrates

This project shows an operational problem solved end to end with Microsoft's agent
tooling: grounded data, multi-step reasoning with real domain methods, quantified
recommendations, action into an external system, and a governance posture that keeps a
human in control. It reflects how I think about applying AI in operations, usefully,
honestly, and with the people who do the work kept firmly in the loop.

*All data and scenarios are fictional, for demonstration only.*
