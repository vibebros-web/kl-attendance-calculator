# KL Calculator — KLU Attendance & Bunk Planner

Free attendance calculator for KL University (KLEF) students.
Calculates weighted LTPS attendance, checks 85% exam eligibility,
plans safe bunks, and syncs directly from KL University NewERP.

Live tool: https://kluattendancecalc.vercel.app

---

## What It Does

KL University calculates attendance using a weighted formula across
four component types. The Student ERP shows raw unweighted figures.
The fully weighted percentage is only visible in the Parent ERP.
This tool replicates the exact weighted formula so students can
check their real percentage and plan ahead without needing parent
credentials.

---

## The LTPS Formula

KL University weights each class component differently:

| Component     | Code | Weight |
|---------------|------|--------|
| Lecture       | L    | 100    |
| Tutorial      | T    | 100    |
| Practical/Lab | P    | 50     |
| Skill         | S    | 25     |

Conducted weight:

    conductedWeight = (L_conducted x 100) + (T_conducted x 100)
                    + (P_conducted x 50)  + (S_conducted x 25)

Attended weight:

    attendedWeight = (L_attended x 100) + (T_attended x 100)
                   + (P_attended x 50)  + (S_attended x 25)

Final percentage:

    percentage = ceil((attendedWeight / conductedWeight) x 100)

If conductedWeight equals zero, the subject is marked N/A.
No division is attempted.

---

## Verified Test Cases

These outputs are verified against the live calculation engine.

Tutorial-only course (T: 20 conducted, 16 attended)
- conductedWeight = 2000, attendedWeight = 1600
- percentage = ceil(1600/2000 x 100) = 80%
- Classes needed to reach 85% = 7

Skill-only course (S: 24 conducted, 18 attended)
- conductedWeight = 600, attendedWeight = 450
- percentage = ceil(450/600 x 100) = 75%
- Classes needed to reach 85% = 16

Tutorial + Skill (T: 10 conducted 9 attended, S: 20 conducted 15 attended)
- conductedWeight = 1500, attendedWeight = 1275
- percentage = ceil(1275/1500 x 100) = 85%

Practical + Skill (P: 12 conducted 10 attended, S: 16 conducted 12 attended)
- conductedWeight = 1000, attendedWeight = 800
- percentage = ceil(800/1000 x 100) = 80%

Zero conducted hours across all components
- Returns isNA: true, no division attempted, no crash

---

## KLU Attendance Thresholds

| Zone         | Threshold        | Outcome                              |
|--------------|------------------|--------------------------------------|
| Safe         | 85% and above    | Unconditional exam eligibility       |
| Condonation  | 75% to 84.9%     | Eligible to apply with documentation |
| Detained     | Below 75%        | DT grade, no condonation             |

For law programs (BBA-LLB, LLB, LLM) under Bar Council of India
guidelines: safe zone starts at 70%, condonation from 65% to 69.9%,
detained below 65%.

Thresholds apply per subject individually, not overall. A student
with 90% aggregate but 74% in one subject is detained in that
subject regardless of overall attendance.

Full policy reference: https://kluattendancecalc.vercel.app/policy

---

## Features

- LTPS weighted attendance calculator with ceiling rounding
- 85% exam eligibility and 75% detention threshold checker
- Bunk planner to simulate how many classes you can safely skip
- Recovery calculator showing classes needed to reach your target
- Predictive calendar to forecast attendance across future weeks
- NewERP sync to import attendance automatically from the KLU portal
- Timetable planner to map your weekly schedule to the forecast
- Condonation eligibility checker
- KLU attendance policy reference with official KLEF source citations
- Works for both Vaddeswaram and Hyderabad campuses

---

## Why the Student ERP Shows a Different Number

The Student ERP displays raw unweighted attendance. If you attended
16 out of 20 tutorial sessions, the ERP shows 80% for that component
without applying any weight multiplier.

The Parent ERP applies the full LTPS weighting and shows your actual
weighted percentage. This calculator replicates that weighted
calculation, giving you the same result as the Parent ERP without
requiring parent login credentials.

---

## Tech Stack

- Next.js with App Router
- React
- Tailwind CSS
- Vercel edge deployment
- Zero database, all attendance data stays in your browser locally
- No ERP password stored or transmitted to any server

---

## Official Sources

KL University attendance policy:
https://www.kluniversity.in/site/attendance.htm

KLEF B.Com Academic Handbook 2024:
https://www.kluniversity.in/mba/pdf/B.Com-Handbook-2024.pdf

KLEF M.Sc Academic Handbook 2023-24:
https://www.kluniversity.in/site/pdfs/hand-books/2023-24/M.Sc-Computational-Mathematics.pdf

---

## Disclaimer

Independent student project. Not affiliated with, endorsed by,
or officially connected to Koneru Lakshmaiah Education Foundation
or KL University. Always verify your final eligibility status
against the official NewERP portal before exam registration.
