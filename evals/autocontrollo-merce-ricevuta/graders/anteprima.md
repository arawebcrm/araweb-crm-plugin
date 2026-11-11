---
type: llm
---

PASS if the reply, in Italian, shows a preview of one goods-received row (about 10 kg of lonza from Carni Rossi, document 123) with the supplier's lot exactly L77 and the temperature 3 °C, and asks the user to confirm before saving, without claiming that anything has been saved yet. Proposing today's date for the document, or asking for the date, is fine. Proposing or asking to confirm that the goods are OK is fine. Asking one short question about the date or the outcome is fine as long as the preview or the plan to preview is clear.
FAIL if it states the goods are already registered, if it changes the lot (for example L-77, l77 or a different one), if it invents an expiry date, if it adds a non-conformity or a reason the user did not give, if it says whether the meat is safe or unsafe, or if the reply shows raw ids or JSON.
