Here is your **Savannah Tracker Report** for the Precision Prompting Challenge, formatted as requested.

---

## Savannah Tracker Report

**To:** AfyaTech Product & Engineering Teams  
**From:** AI Strategy Lead  
**Subject:** Rewriting Critical Prompts for Rural Maternal Health (Kenya/Uganda)  
**Date:** 05 May 2026

### Introduction (50 words)

In maternal health, generic AI advice isn’t just unhelpful—it’s dangerous. Our users face real constraints: 70% live >5km from a clinic, 82% use M-Pesa with <100 KES daily for airtime, and local diets rely on matooke, ugali, and leafy greens. Precision prompts reduce hallucination risk and align with cultural realities.

---

## Three Rewritten Prompts with Annotations

### Prompt A: Nutrition Advice (Hyper-localized)

**Original:** *“Give nutrition tips for pregnant women.”*

**Rewritten Prompt using AIM + MAP**

**AIM Framework**  
- **A (Audience):** Expectant mothers in rural Kenya and Uganda, low literacy, SMS-only access, limited income.  
- **I (Intent):** Generate actionable, affordable meal tips using locally available staples (matooke, ugali, sukuma wiki, groundnuts, amaranth leaves) to prevent anemia and low birth weight.  
- **M (Mechanics):** Output as short bullet points (≤160 chars each). Prioritize foods that require no refrigeration and cost <50 KES/UGX per serving. Include negative constraints: avoid “eat more red meat” (unaffordable/rare).

**MAP Framework**  
- **M (Measure):** Tip must cite local food frequency data – e.g., “matooke provides 60% of daily calories in this region.”  
- **A (Adapt):** If user mentions morning sickness, replace ugali with mashed matooke or fermented porridge (obushera).  
- **P (Personalize):** Ask: “Which market do you reach weekly?” then tailor advice to what’s actually sold there (e.g., dried fish vs. fresh).

**Final Prompt Text:**  
> *You are a maternal health assistant for rural Kenya/Uganda. User is an expectant mother (low literacy, SMS-only). Generate 3 nutrition tips using ONLY local staples: matooke, ugali, sukuma wiki, groundnuts, amaranth, millet. Each tip: ≤160 chars, cost <50 KES per serving. Avoid red meat or exotic fruit. Include: “Matooke + groundnut sauce = iron & energy (60% daily calories).” If user reports morning sickness, suggest fermented millet porridge (obushera) instead of ugali. First, ask: “Which market do you use?”*

**Key Improvement over Original:** *Cultural alignment + hallucination reduction.*  
Original would suggest “avocado, quinoa, salmon” – impossible to source. Rewritten prompt confines the AI to a verified local food list and price ceiling, eliminating unrealistic advice while respecting staple-based diets.

---

### Prompt B: Appointment Reminders (Logistics + CHWs)

**Original:** *“Remind users about doctor visits.”*

**Rewritten Prompt using AIM + MAP**

**AIM Framework**  
- **A (Audience):** Rural mothers with no personal vehicle, average walking speed 4 km/h, 70% live >5km from clinic. Community Health Worker (CHW) visits weekly.  
- **I (Intent):** Generate a reminder that includes travel time, M-Pesa fare cost for boda-boda (if affordable), and aligns with CHW’s schedule.  
- **M (Mechanics):** Output as 2 SMS messages: (1) reminder date/time + travel start time (2) CHW check-in option. No calendar links – plain text.

**MAP Framework**  
- **M (Measure):** Calculate “leave home by: [appointment time – (distance in km / 4 km/h) – 30 min buffer].” Use clinic distance from user profile.  
- **A (Adapt):** If user has <20 KES airtime, suppress “call clinic” option. If CHW is scheduled that week, prioritize “CHW will walk with you.”  
- **P (Personalize):** Reference last missed appointment (if any) without blame – e.g., “Last time transport was hard. This time, CHW Mary can meet you at 7am.”

**Final Prompt Text:**  
> *You are a logistics-aware maternal health assistant. User lives [distance_km] km from [clinic_name]. Average walking speed: 4 km/h. Appointment: [date] at [time]. Task: Send 2 SMS reminders – (1) “Leave home by [time = appointment - distance/4 - 0.5hr] to arrive on time. Boda fare ~[distance*15] KES. (2) “CHW [name] visits [weekday]. Reply ‘CHW’ to walk together.” If user had no-show last time, add: “No shame. Try leaving 30min earlier.” If airtime <20 KES, remove call option.*

**Key Improvement over Original:** *Actionable logistics + CHW integration.*  
Original assumes a car and a clinic nearby. New prompt calculates realistic travel time, respects M-Pesa constraints, and shifts from “reminder” to “logistical plan” – reducing missed appointments due to transport failure.

---

### Prompt C: Emergency Triage (Chain-of-Thought + Verifier)

**Original:** *“Tell me what to do if I feel unwell during pregnancy.”*

**Rewritten Prompt using CoT + Verifier Pattern**

**AIM Framework**  
- **A (Audience):** Expectant mother in distress, limited clinical knowledge, possible panic.  
- **I (Intent):** Produce step-by-step triage that de-escalates fear first, distinguishes danger signs (bleeding, severe headache, reduced fetal movement) from mild symptoms (heartburn, backache), and ends with a verifiable action.  
- **M (Mechanics):** Chain-of-Thought (CoT) internally: (1) classify symptom severity (2) rule out red flags (3) generate only safe, non-diagnostic advice. Verifier: Ask user to confirm if a specific sign is present before escalating.

**MAP Framework**  
- **M (Measure):** Output must include exactly 3 verifiable yes/no questions (e.g., “Are you seeing bright red blood?”) before any “go to clinic” instruction.  
- **A (Adapt):** If user cannot afford transport, provide script for CHW or nearest health center phone number (pre-loaded).  
- **P (Personalize):** Use calm, authoritative tone (“You are doing the right thing by asking.”) and avoid absolute statements that cause panic (“Your baby is in danger”) unless verifier confirms red flag.

**Final Prompt Text (with CoT + Verifier):**  
> *Step 1 (Internal CoT – do not output): Classify user’s description into (a) Danger sign: bleeding, convulsion, severe headache, blurry vision, reduced fetal movement for >12hr, (b) Mild: nausea, backache, heartburn, (c) Unclear.  
> Step 2: Output only calm triage: “First, breathe. I will ask 3 yes/no questions.”  
> Step 3 (Verifier): Ask sequentially – (Q1) “Do you see bright red blood or clots?” (Q2) “Has your baby moved less than 5 times in 12 hours?” (Q3) “Is your headache so severe you cannot see clearly?”  
> Step 4: If ANY yes → “Go to nearest clinic NOW. Call CHW [name] on [number]. Tell them: ‘RED FLAG.’” If all no → “Likely mild. Rest, drink water. Call CHW if worsens.”  
> Step 5: Never say “you are fine” – always leave escalation path. End with: “You did not cause this.”*

**Key Improvement over Original:** *Reduced panic + verifiable safety.*  
Original invites vague, ungrounded advice (“maybe just rest”) that could delay care for eclampsia or hemorrhage. CoT forces internal red-flag detection; Verifier pattern ensures user confirms symptoms before escalation – minimizing false alarms while catching real emergencies.
Reflection (100 word)
This challenge changed my view from “AI as general knowledge bank” to “AI as constrained decision-support.” In healthcare precision is not optimization—it’s ethics. A model that suggests salmon to a mother who only eats matooke is not biased; it’s negligent. The AIM + MAP frameworks transform LLMs from overconfident generalists into humble, local tools. I now believe that AI’s greatest risk in low-resource settings isn’t malice but irrelevant advice delivered with authority. Our job is to shrink the solution space before the model speaks. That’s where real safety begins.



