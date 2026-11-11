---
type: llm
---

PASS if the reply, in Italian, tells the user that guanciale is not among the products already in the registers and asks whether to add it (for example as a new product, unit kg) before registering the delivery, keeping the data given (Carni Rossi, DDT 130, 5 kg, lot G-8841, 2 °C) for the next step. It must not claim that the product or the delivery has been saved.
FAIL if it says the product has been created or the delivery registered, if it silently maps guanciale to another product (such as Lonza di maiale), if it changes or invents the lot, an expiry date or a reason, if it says whether the food is safe, or if the reply shows raw ids or JSON.
