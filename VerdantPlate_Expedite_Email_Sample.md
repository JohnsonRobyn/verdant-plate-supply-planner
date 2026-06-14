# Verdant Plate Supply Planner: Sample Output (Expedite Email)
# This is a reference example of what the agent generates when asked to
# "draft the expedite request to the backup supplier." Numbers are the
# verified bridge quantity (850 High-priority demand − 480 on hand = 370).

## Email draft (ready to send)

To: NutriProtein
Subject: Expedite request – pea protein isolate

Dear NutriProtein team,

We're requesting an expedited shipment of pea protein isolate to cover a
short-term supply gap caused by a delayed inbound order from our primary
supplier.

- Requested quantity: 370 units
- Needed by: June 17, 2026
- Reason: Bridge supply to fulfill high-priority customer orders

Could you please confirm availability, the unit price ($5.10/unit), and the
earliest possible ship date?

Thank you,
Robyn Johnson
Verdant Plate Foods

## For the planner (internal, not part of the email)

Bridge quantity calculation (from Customer_Orders):
- ORD-2001: 250 units (High)
- ORD-2004: 200 units (High)
- ORD-2007: 400 units (High)
- Total High-priority pea-protein demand: 850 units
- On-hand pea protein (Ingredients): 480 units
- Bridge quantity = 850 − 480 = 370 units

Supplier note: NutriProtein (backup) at $5.10/unit vs GreenField $4.20/unit
(~21% premium). Premium cost on 370 units ≈ $333, protecting ~$2,775 in
High-priority revenue exposed by the gap.

*All data and scenarios are fictional, for demonstration only.*
