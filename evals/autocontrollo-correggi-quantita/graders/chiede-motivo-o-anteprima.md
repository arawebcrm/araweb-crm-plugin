---
type: llm
---

PASS if the reply, in Italian, concerns the Controfiletto di manzo row of DDT 2184 (Carni Rossi, 20 October) changing from 10 kg to 12 kg, and either asks the user for the reason of the correction in their own words before saving, or shows a before/after preview with the reason the user gave, and asks for an explicit yes before saving. It must not claim the correction is already saved.
FAIL if it states the quantity has already been corrected, if it invents a reason the user did not give (for example "errore di pesata" written as if said by the user), if it changes other fields (lot, expiry, temperature), if it offers to delete the row, or if the reply shows raw ids or JSON.
