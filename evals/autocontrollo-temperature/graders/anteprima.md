---
type: llm
---

PASS if the reply, in Italian, shows a preview of exactly two readings (Frigo cucina 3 °C and Congelatore -19 °C, both within limits, with the limits or the "nei limiti" outcome), says these are the user's own values or the morning (first) reading, and asks the user to confirm before saving, without claiming that anything has been saved yet. Mentioning that other readings are still missing (for example the second fridge reading today or the days 20 and 21 October) without inventing values for them is fine.
FAIL if it states the readings are already saved, if it changes or rounds the values, if it adds values the user did not give, if it tells the user whether the food is safe, or if the reply shows raw ids or JSON.
