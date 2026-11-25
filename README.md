# AI Support Agents in Production

**SuperEvent · December 2025 – present**
**Vibe Harboe, AI & Automation Specialist**

AI agents answer customers on all five of SuperEvent's service websites. They answer only what the knowledge base can back up and hand everything else to a person. I run them like a product: measure, test, improve, every week.

This repository is a case write-up, not source code. The agents run on a commercial platform (HelpCrunch). Instructions, flow design and internal tooling stay with SuperEvent.

## At a glance

| | |
|---|---|
| **Live on** | 5 of 5 service websites: BreakoutRoom.dk, EventCenter.dk, CityMeetings.dk, SuperLej.dk and SuperEvent.dk |
| **Resolved without a person** | About 56 % of closed chats (150 of 266), December 2025 to October 2026, own measurement |
| **The platform's own "resolved" counter** | 1 of 139, over the same months |
| **My role** | Sole builder and owner of operations: bot flows, agent behaviour, escalation rules, knowledge base, measurement and the weekly improvement loop |
| **Tools** | HelpCrunch AI agents, bot flows, knowledge base design, Python |

Volumes are modest, so every number here is shown with its count and its period.

## The problem

SuperEvent runs several event and rental brands, each with its own website and the same kind of repeat questions: prices, availability, directions, practical details. Every chat landed with a person, also the ones a good answer could close on the spot.

The goal was not a chatbot that always answers. It was an agent that gives a solid answer when it can back one up, and a person when it can't.

## What I built

- **AI agents on five websites.** One agent per brand, grounded in a curated knowledge base. When an answer can't be backed up, the agent says so and hands over instead of guessing.
- **Bot flows and escalation rules.** The flows and rules that decide when the agent answers and when a person takes over, so customers get either a solid answer or a human.
- **Independent measurement.** A baseline across every chat since launch, a catalogue of the questions the agents couldn't answer, a Python monitor and a weekly archive, because the platform keeps only 30 days of data.
- **Knowledge base hygiene.** A Python sweep that checks every article for outdated prices, duplicates, contradicting facts, wrong email addresses, empty articles and broken links, before customers find them.
- **A test discipline.** Every change is tested against real customer questions, with a clean chat history before each question, at least three runs, and several phrasings and languages.

## The finding that changed the project

Months into operation, the platform reported that the flow had resolved 1 chat out of 139.

I didn't trust the number, so I built my own baseline across every chat since launch. It showed that about 56 % of closed chats were resolved without a person.

The difference came from how the platform counts. A chat only counted as resolved if the customer actively confirmed it. Most satisfied customers simply get their answer and leave, and those were counted as abandoned. The counter wasn't measuring resolution at all.

We were about to optimise content against a number that measured nothing. The rule I took from it: **fix the instrumentation before the content.**

## The weekly loop

1. **Measure.** What did the agents resolve, refuse or hand over?
2. **Find the gap.** Missing knowledge, unclear wording or a flow that leaks.
3. **Fix and test.** Against real customer questions, in several phrasings and languages.
4. **Report.** A running decision list for management, and lessons written up for the next agent project.

## What operations taught me

**What the agent retrieves beats what it is told.** When the knowledge base and an instruction disagreed, the knowledge base won, each of the five times we tested it. So a rule that must hold belongs in the content, and a wrong answer usually means a missing article, not a missing rule.

**Refusals are invisible in standard reports.** "I can't find the answer" looks like correct behaviour, so it never shows up as an error. I built a catalogue of 68 refusals in three categories and worked through them one by one. It is the most expensive error type, and it has to be counted on its own.

**Fewer than half of the chats routed to a person actually wanted one.** In the first flow, 31 of 67 routed chats said yes when asked if they wanted a person. Asking before handing over roughly halves the load on the team.

**One green test proves nothing.** The same question, asked three times with a clean history, gave a full answer, an empty reply and an escalation. That is why nothing is called fixed before at least three runs.

**Clear your own setup before blaming the vendor.** Three of the four problems we suspected were platform bugs turned out to be our own configuration. The fourth was real: an empty reply bubble. I sent HelpCrunch a controlled test with a chat ID they could look up. They confirmed the bug the same day and passed it to their developers.

**Withdraw a claim that doesn't hold.** I reported that the refusal rate was rising. When I checked the baseline again, the first month covered only two days of operation, so the "rise" had never happened. I withdrew the claim. A partial first month is not a baseline.

## What I would tell the next team

- Decide what "resolved" means before you launch, and check that the platform measures the same thing.
- Put the facts that change (prices, availability) on the website and let the knowledge base point to them. Put the facts that don't change in the knowledge base.
- Treat every correct handover as work for a person. If no one picks it up, it looks like a bot failure.

## What this repository does not contain

The agents' instructions, the flow design, the source configuration and the internal tools. They belong to SuperEvent, and they are the part that makes the setup work.

## Contact

**Vibe Harboe** · AI & Automation Specialist
[vibeharboe.dk](https://www.vibeharboe.dk) · [LinkedIn](https://www.linkedin.com/in/v-h-c) · [GitHub](https://github.com/VibeHarboe) · vibeharboe@gmail.com
