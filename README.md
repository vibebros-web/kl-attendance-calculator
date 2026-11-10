# KL Attendance Calculator: KLU LTPS Attendance, Bunk Planner & KL Timetable

**A free, unofficial attendance calculator and timetable planner for KL University (KLU / KLEF) students.**

It calculates weighted LTPS attendance, shows how many classes you can skip, estimates how many classes you need to recover, and plans your week with a built-in timetable.

**Live app: https://kluattendancecalc.vercel.app**

*Last updated: November 2026*

> Unofficial student tool and planning aid. Your parent ERP is always the official figure. See the [disclaimer](#disclaimer).

---

## Pages

| Page | What it is |
|---|---|
| [Home / dashboard](https://kluattendancecalc.vercel.app) | Per-subject attendance, status, skip margin and classes needed |
| [Import from NewERP](https://kluattendancecalc.vercel.app/uploads) | ERP sync or paste your attendance and timetable |
| [KL Timetable planner](https://kluattendancecalc.vercel.app/timetable) | Weekly timetable, Monday to Saturday |
| [Bunk planner / forecast](https://kluattendancecalc.vercel.app/forecast) | Forecast attendance to a date and find safe days off |
| [LTPS calculator and formula](https://kluattendancecalc.vercel.app/ltps) | Weighted attendance explained |
| [TCBR guide and calculator](https://kluattendancecalc.vercel.app/tcbr) | Total Classes Before Registration |
| [Recovery guide and calculator](https://kluattendancecalc.vercel.app/recovery) | Classes needed to reach 75% or 85% |
| [Methodology](https://kluattendancecalc.vercel.app/methodology) | The formulas used |
| [Attendance guide](https://kluattendancecalc.vercel.app/guide) | 85% rule, 75% condonation floor, safe bunks |
| [Condonation](https://kluattendancecalc.vercel.app/condonation) | Eligibility and process |
| [Attendance policy](https://kluattendancecalc.vercel.app/policy) | Rules with links to official KLEF documents |

---

## Features

### Attendance
- LTPS weighted attendance (Lecture, Tutorial, Practical, Skill) with ceiling rounding
- Per-subject cards with a component breakdown
- Shows how many classes you can skip, or how many you need to reach your target
- Target toggle between 75% and 85%
- TCBR mode on or off
- Status labels: Safe (85%+), Condonation (75-84%), Below 75%
- Add or remove simulated classes to preview the effect before it happens
- Banner when your synced data is more than 24 hours old

### Bunk planner (forecast)
- Pick an end date and a target from 76% to 95%
- Mark days as absent or holiday on a calendar
- Dots show what would happen if you missed a given day
- "Find Safe Days Off" suggests combinations of days off, ranked by least impact
- Projected Impact card compares current and projected percentage per subject
- Uses your timetable, so projections follow your real class days

### KL Timetable planner
- Weekly grid, Monday to Saturday
- Shows course code, component (Lecture, Tutorial, Practical, Skill), room and section
- Import from NewERP or build from scratch
- Tap a cell to pick a subject, set the component, edit the room, or clear the slot
- Color-coded by component
- Show periods automatically or up to 24
- Weekly load summary grouped by subject and component

### Calculators (no import needed)
- LTPS weighted calculator
- TCBR calculator: result with and without TCBR
- Recovery calculator: classes needed to reach 75% or 85%

### Importing your data
- **ERP sync** with your student ID, password and captcha
- **Paste** the ERP attendance or timetable page, with a step-by-step tutorial
- Or enter things yourself

### App
- Installable as a PWA
- Dark mode
- Mobile layout with bottom navigation
- Clear attendance, timetable, or absences and holidays separately

---

## The LTPS formula

KL University attendance is weighted by component:

| Component | Code | Weight |
|---|---|---|
| Lecture | L | 100 |
| Tutorial | T | 100 |
| Practical / Lab | P | 50 |
| Skill | S | 25 |

```
conductedWeight = (L_conducted x 100) + (T_conducted x 100)
                + (P_conducted x 50)  + (S_conducted x 25)

attendedWeight  = (L_attended x 100) + (T_attended x 100)
                + (P_attended x 50)  + (S_attended x 25)

percentage = ceil((attendedWeight / conductedWeight) x 100)
```

If `conductedWeight` is zero, the subject is shown as N/A and no division is attempted.

### Worked examples

| Case | Result |
|---|---|
| Tutorial only: 20 conducted, 16 attended | 80%, 7 more classes to reach 85% |
| Skill only: 24 conducted, 18 attended | 75%, 16 more classes to reach 85% |
| T: 10 conducted, 9 attended; S: 20 conducted, 15 attended | 85% |
| P: 12 conducted, 10 attended; S: 16 conducted, 12 attended | 80% |

### Recovery estimate

```
classesNeeded = ceil((target x conducted - attended) / (1 - target))
```

For example, 58 attended out of 70 conducted needs 10 more classes to reach 85%.

Full details: [methodology page](https://kluattendancecalc.vercel.app/methodology).

---

## Attendance thresholds

| Zone | Threshold | Usual outcome |
|---|---|---|
| Safe | 85% and above | Eligible for exams |
| Condonation | 75% to 84% | Discretionary, never automatic; apply with documentation |
| Below 75% | Under 75% | Usually detained |

Thresholds are applied per subject. Different thresholds apply to some programs, such as law. Confirm with your department office.

Policy reference: [attendance policy](https://kluattendancecalc.vercel.app/policy) · [condonation guide](https://kluattendancecalc.vercel.app/condonation)

---

## FAQ

**How is KL University attendance calculated?**
By component weights: Lecture and Tutorial at 100, Practical at 50 and Skill at 25. See the formula above.

**What attendance do I need at KL University?**
85% is the safe level. Between 75% and 84%, condonation may be possible with documentation. Below 75% you are usually detained. Confirm with your department office.

**What is TCBR?**
Total Classes Before Registration. The parent ERP subtracts these classes in its LTPS calculation. This tool lets you view your result with TCBR on or off. See the [TCBR guide](https://kluattendancecalc.vercel.app/tcbr).

**How many classes do I need to attend to reach 85%?**
Use the [recovery calculator](https://kluattendancecalc.vercel.app/recovery) or the formula above.

**How many classes can I skip?**
Use the [bunk planner](https://kluattendancecalc.vercel.app/forecast). It forecasts to a date you choose and can suggest safe days off.

**Is this official?**
No. It is an independent student project. Your parent ERP is the official figure.

**Where is my data stored?**
Attendance and timetable data are saved in your browser (localStorage). For ERP sync, the app's server fetches your data from NewERP and returns it to your browser. It does not save your password or attendance records in a database. The site uses Google Analytics.

---

## Tech stack

- Next.js (App Router)
- React
- Tailwind CSS
- Serwist (PWA)
- Deployed on Vercel
- No database; saved data lives in your browser

---

## Official sources

- KL University attendance page: https://www.kluniversity.in/site/attendance.htm
- Attendance Policy and Evaluation Process (PDF): https://www.kluniversity.in/site/pdfs/Attendance-Policy-and-Evaluation-Process.pdf

---

## Disclaimer

Independent student project. Not affiliated with, endorsed by, or officially connected to Koneru Lakshmaiah Education Foundation or KL University. All figures are estimates for planning. Always check your final eligibility against the official NewERP portal and your department office before exam registration.
