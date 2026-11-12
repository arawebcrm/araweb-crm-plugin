---
type: llm
---

PASS if the reply, in Italian, asks the user why the mozzarella is non-conforming (the reason in the user's own words, for example damaged packaging, temperature, rejected) before registering it, or it shows a preview only after the user gave a reason. It must not have saved anything yet.
FAIL if it registers the row, if it invents or suggests a reason and writes it as if the user had said it (for example "imballo rotto" or "temperatura alta"), if it quietly marks the row OK, if it says whether the product is safe or must be thrown away, or if the reply shows raw ids or JSON.
