# LanaStudyBot

**A working Telegram MVP for teenage educational and career decision support, built as the first user-facing module of the broader Eidos product concept.**

LanaStudyBot helps teenagers move from a vague “I don’t know what fits me” to a structured first profile that can be discussed with a parent or career-guidance specialist.

The current version is intentionally focused: a short conversational flow, deterministic profile calculation, visual result cards, lightweight product analytics, a clear route to human consultation, and a separate free-gift flow after the result.

> **Product principle:** technology should help structure a decision, not pretend to make the decision for a person.

**Live Telegram bot:** https://t.me/LanaStudyMVP_bot  
**Project channel:** https://t.me/mesto_resheniy

> This repository is intended as a public product case study and technical overview. Production source code, real user data and proprietary scoring methodology are intentionally not published.

---

## Product context

LanaStudyBot started as an MVP for testing a practical question:

**Can a lightweight digital interaction help a teenager understand themselves better and make the next conversation about education more concrete?**

The bot is not positioned as a final career choice and does not replace a specialist. It provides a first structured profile and creates a starting point for further exploration.

The product also acts as a practical prototype for **Eidos**, a broader decision-support platform concept for educational and career choices.

This public repository focuses on LanaStudyBot as a standalone Telegram MVP and on its product and technical architecture.

---

## Why I built it

LanaStudyBot grew out of a real problem I faced as a parent: how to help a teenager make an educational choice without pressure and without starting from “Which profession should you choose?”

Going through this journey with my daughter showed me that a better starting point is the teenager themselves - their interests, strengths, preferred activities and environment.

That experience later became one of the foundations for **Mesto Resheniy / Land of Decisions** and, eventually, the broader **Eidos** concept.

---

## Current user flow

```text
/start
  ↓
Introduction
  ↓
16-question conversational questionnaire
  ↓
Single-choice / multiple-choice answers
  ↓
Deterministic scoring
  ↓
Primary profile + additional profile
  ↓
Short result summary
  ↓
4 visual result cards
  ↓
Additional-profile explanation
  ↓
Human consultation / restart
  ↓
Optional free gift
  ↓
Subscribe to “Mesto Resheniy”
  ↓
Subscription verification
  ↓
“Trajectory” PDF guide
```

The main experience stays inside Telegram and avoids the feeling of filling in a long external form.

A key UX decision in the current version is that **the result is not gated by subscription**. Once the questionnaire is completed, the user immediately receives the useful result and four visual cards.

The cards cover:

1. **Profile**
2. **Strengths**
3. **Directions to explore**
4. **Suitable environment**

When relevant, the user also receives an explanation of the additional profile.

The cards are designed to be easy to save, share, or use as a conversation starter with a parent or specialist.

---

## Result delivery and next step

After questionnaire completion, the bot:

1. calculates the primary and additional profile;
2. maps the primary profile to the relevant materials;
3. immediately shows the result summary;
4. sends four visual result cards in a fixed sequence;
5. adds the additional-profile explanation;
6. offers a **human result-review step**;
7. keeps a restart option for further exploration;
8. separately offers a free **Trajectory** mini-guide;
9. verifies membership in the **Mesto Resheniy** Telegram channel through the Telegram Bot API;
10. sends the PDF gift after successful verification.

The **Discuss my result** action opens Telegram with a pre-filled message that already includes the user’s primary profile. This reduces friction between a digital result and a real conversation with a specialist.

Restart is intentionally preserved as an exploration mechanism: users can compare how different answers change the outcome without using a “Back” button to optimise answers within the same run.

The free guide is deliberately separated into a post-result flow. Subscription is no longer a condition for receiving the main result; it is connected to additional value.

---

## Product analytics and admin tools

The MVP includes a lightweight internal analytics layer.

### Data stored

The application keeps separate records for:

- users;
- raw questionnaire answers;
- calculated profile results;
- product events;
- first-touch acquisition source.

This separation is deliberate: raw behavioural data can be analysed independently from the current interpretation logic.

### Events currently logged

```text
survey_started
question_answered
survey_completed
```

This makes it possible to analyse the questionnaire as a product flow rather than only store final results.

### Funnel measurement

The admin layer exposes:

- total users;
- unique completions;
- total result records;
- questionnaire starts;
- questionnaire completions;
- completion rate.

Event instrumentation was added incrementally during early MVP testing. Historical totals and event-based funnel metrics are therefore interpreted separately, and the current completion rate is treated as a diagnostic metric rather than a final production KPI.

### Traffic-source attribution

Telegram deep links are used for first-touch acquisition attribution.

Example sources:

```text
instagram
telegram_channel
vk
linkedin
direct
```

Example:

```text
https://t.me/LanaStudyMVP_bot?start=instagram
```

The first recorded source is preserved and is not overwritten by later visits from the same user.

### Admin commands

The current admin-only toolkit includes:

```text
/ping
/status
/sources
/export
```

It supports:

- operational health checks;
- user and result statistics;
- product-funnel monitoring;
- traffic-source counts;
- CSV export for further analysis.

The admin layer is deliberately lightweight at the MVP stage: the goal is to collect enough evidence to improve the product without building a large back-office system too early.

---

## What we learn from user behaviour

LanaStudyBot is used not only as an assessment tool but also as a source of product learning.

Behavioural observations and user feedback help distinguish:

- assumptions made during questionnaire design;
- options users actually select;
- questions that provide useful differentiation;
- wording that needs to be rewritten or removed;
- mobile UX friction;
- reactions to result delivery and calls to action.

The first test group is still small, so qualitative feedback is treated as an early signal rather than statistical proof of assessment accuracy.

Early testing has already highlighted the value of:

- a short and understandable flow;
- visual result cards;
- repeat completion for comparison;
- the result as a conversation starter;
- shorter wording for mobile screens;
- delivering the main result **before** any subscription request;
- using a separate free gift as a clearer value exchange.

---

## Architecture

The bot is intentionally modular.

```text
Telegram
  ↓
Handlers / FSM
  ↓
Questionnaire scenarios
  ↓
Scoring service
  ↓
Result delivery service
  ↓
CTA / consultation
  ↓
Bonus + subscription verification
  ↓
Visual / PDF materials
  ↓
SQLite storage
  ↓
Analytics / admin export
```

A simplified project structure:

```text
handlers/
keyboards/
scenarios/
services/
states/
storage/
texts/
materials/
tests/
```

The exact scoring rules and proprietary methodology are not part of the public description.

---

## Technology

Current implementation:

- **Python**
- **aiogram**
- **Telegram Bot API**
- **FSM-based conversational flow**
- **SQLite**
- **Git**
- **Linux VPS**
- **systemd**
- modular handlers, services, scoring, storage, scenarios and result-delivery components

The solution is deployed and tested on my own server.

The production bot runs as a `systemd` service, starts automatically after server reboot and does not depend on a local development machine remaining online.

AI tools are used as part of the development workflow for analysis, implementation support, testing and documentation, while the current user-profile calculation remains deterministic and testable.

---

## AI-assisted development workflow

An important part of this project is not only the product itself but also the way it is being built.

For the latest MVP iteration I used a lightweight AI-assisted workflow:

```text
legacy analysis
      ↓
content / product logic
      ↓
implementation
      ↓
QA
      ↓
user feedback
      ↓
UX iteration
```

The repository and project documentation act as shared context between these roles.

I deliberately avoided building a complex agent framework around a relatively small MVP. The goal was to use AI where it reduced analysis and implementation time while keeping product decisions, acceptance criteria and final verification under human control.

> **AI-assisted development is not the same as putting an LLM inside every feature.**

The current assessment engine is intentionally deterministic because transparency, repeatability and testability matter more than novelty at this stage.

---

## Current status

The MVP currently supports:

- an end-to-end 16-question Telegram flow;
- single- and multiple-choice interactions;
- deterministic primary and additional profile calculation;
- immediate visual result delivery;
- four primary-profile result cards;
- additional-profile explanation;
- a human-consultation CTA;
- questionnaire restart;
- a separate post-result gift flow;
- subscription verification through the Telegram Bot API;
- free PDF delivery after successful verification;
- storage of users and raw answers;
- separate storage of calculated results;
- product-event logging;
- lightweight funnel measurement;
- first-touch traffic-source attribution;
- admin health/status/source checks;
- CSV export;
- 24/7 deployment through `systemd` on a Linux VPS.

The first small group of users has already provided qualitative feedback on usability, perceived result relevance, mobile readability and the usefulness of the visual cards.

---

## Product decisions already validated in the MVP

### 1. No “Back” button in the questionnaire

A “Back” button was considered but deliberately not added.

The questionnaire is designed to capture the user’s first reaction rather than encourage optimisation towards a preferred outcome.

Users who want to experiment can restart the questionnaire and compare the result.

### 2. Deliver the core value first, then offer additional value

In an earlier version, the extended result was tied to mandatory subscription.

User testing led to a UX change: the bot now **delivers the result and all four cards immediately**, while subscription appears only in the separate free-guide flow.

This reduces friction and makes the value exchange clearer: the user has already received the core result, and subscription is required only for the additional resource.

### 3. Keep a human specialist in the loop

After the result, the primary CTA leads to a human review rather than another automated step.

This reflects the core product principle: the digital layer structures information, while complex context and the final decision remain part of a human-in-the-loop process.

### 4. Keep raw answers separate from interpretation

Questionnaire answers and calculated profiles are stored separately.

This makes it possible to evolve scoring logic later without losing the original behavioural data.

### 5. Keep the current scoring deterministic

The teenager module does not use an LLM to calculate the profile.

The logic remains deterministic, testable and easier to validate during early product development.

---

## Next improvements

The next iteration is focused on deeper measurement and operational learning rather than adding features for their own sake.

Planned improvements include:

- completion and drop-off analysis by session;
- normalising event-based completion-rate measurement;
- answer-frequency analysis by question, including zero-selection options;
- questionnaire completion time;
- distribution of primary and additional profiles;
- result-to-consultation conversion;
- gift-offer to verified-subscription and bonus-delivery conversion;
- richer source-level funnel analysis;
- tracking selected post-result actions;
- continued refinement of result presentation and calls to action;
- additional monitoring and operational safeguards.

---

## From LanaStudyBot to Lana Decision Bot and Eidos

LanaStudyBot is not intended to become a huge Telegram bot containing every possible feature.

It is being developed as a **standalone teenage module**.

The next separate product module, **Lana Decision Bot**, is planned for adults and will evolve independently with its own audience, scenarios, content, results and positioning.

Over time, reusable components may be extracted into **Eidos** - a broader decision-support platform architecture.

```text
Eidos
future platform
│
├── LanaStudyBot
│   └── teenagers / educational trajectories
│
└── Lana Decision Bot
    └── adults / career and life decisions
```

The broader platform concept follows a simple separation of responsibilities:

```text
Digital layer
collects and structures information
        ↓
Decision-support layer
turns information into understandable scenarios
        ↓
Human specialist
adds context, interpretation and discussion
        ↓
User
makes the decision
```

> **Automation prepares the structure; human conversation handles context, uncertainty and meaning.**

---

## What this project demonstrates

From a professional perspective, LanaStudyBot is an end-to-end product and delivery case.

My role covers:

- product discovery and scope definition;
- user journey design;
- requirements and acceptance criteria;
- questionnaire and result logic;
- modular solution design;
- AI-assisted development workflow;
- implementation coordination and hands-on prototyping;
- deployment on Linux VPS;
- testing and iterative improvement;
- analytics design;
- acquisition measurement;
- user-feedback analysis;
- roadmap and product evolution.

The project reflects how I work at the intersection of **IT project management, product thinking, business analysis, implementation and AI-enabled automation**.

---

## About

**Svetlana Borisenko**  
IT Project Manager / Delivery & Implementation / Product-oriented PM

Background: enterprise software, FinTech, system integrations, process automation and AI-related products.

LanaStudyBot, the planned Lana Decision Bot and Eidos are independent product initiatives used to validate practical approaches to digital decision support and human-in-the-loop services.

---

## Screenshots for the public repository

Recommended structure:

```text
docs/images/
├── 01_bot_start.png
├── 02_question_flow.png
├── 03_result_summary.png
├── 04_profile_card.png
├── 05_strengths_card.png
├── 06_directions_card.png
├── 07_environment_card.png
├── 08_result_actions.png
├── 09_gift_offer.png
├── 10_subscription_check.png
└── 11_gift_pdf.png
```

Before publishing screenshots, remove or blur Telegram usernames, user IDs, email addresses, internal admin data and other personal information.

The public README should show the user experience, product decisions and engineering approach without exposing the proprietary scoring model or real user data.

---

## Live product

**Telegram bot:** https://t.me/LanaStudyMVP_bot  
**Project channel:** https://t.me/mesto_resheniy

> Production source code and proprietary scoring methodology are not publicly available. This repository is intended as a product case study and technical overview.
