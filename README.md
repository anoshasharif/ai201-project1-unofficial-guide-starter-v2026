# The Unofficial Guide

<!-- Replace this line with your name and which corpus you picked. -->

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

I chose the city guides corpus, which contains travel information about different towns and locations. My system retrieves information from these guides to answer questions about attractions, food, places to stay, transportation, and the best times to visit. It uses the most relevant sections of the guides to answer the question and identifies the source of the information. If the documents do not contain enough relevant information, the system is designed to refuse to answer rather than make up information.


## Chunking Strategy

**Chunk size:** Maximum of approximately 1,000 characters

**Overlap:** One previous paragraph is carried forward into the next chunk

I chose this strategy because the city guides are longer documents organized into sections and paragraphs. Instead of splitting the text at a fixed character position, I wanted related information to stay together as complete thoughts. I used a maximum size of about 1,000 characters while splitting at paragraph boundaries, and carried the previous paragraph into the next chunk to preserve context between chunks.

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `guide_accessibility.md#0` — produced by: `chunker.py::split_documents`

# Getting around the region with limited mobility

An honest assessment rather than a promotional one. Some of these places are
difficult and it is better to know in advance.

## Straightforward

**Thornby Wells** is the easiest town in the region. It is flat, compact, and
everything is within three minutes of everything else. Parking is free for two
hours anywhere in town and the station is central. The pump room and gardens
are level throughout.

**Marchwood** has a modern tram network with level boarding on all four lines,
running every 8 minutes on weekdays. The city museum and covered market are both
step-free. The distances between districts are the main consideration.

**Brightwater** is level along the river and through the centre. The mill museum
is step-free. The station is a 15-minute walk from campus on flat ground, or the
shuttle meets the four busiest arrivals.

## Mixed



**Chunk 2** — source: `guide_corry_vale.md#1` — produced by: `chunker.py::split_documents`

## Eat and drink

One pub in the largest village serves food seven days a week. A second, in the third village, opens Thursday to Sunday. There is a farm shop at the valley mouth that sells bread, cheese and little else, and it closes at 4pm. Bring supplies; this is not a place with options.

## What to see

The valley itself is the attraction. The footpath network is dense and well marked, and a circuit taking in three of the four villages is about nine miles with 500 metres of ascent. The chapel in the second village is 12th century and always unlocked.

## Where to stay

Perhaps thirty beds in the entire valley, spread across two pubs and a handful of farmhouse rooms. In summer these are booked months ahead. Camping is permitted on two marked fields and nowhere else.

## When to go




**Chunk 3** — source: `guide_elder_ness.md#2` — produced by: `chunker.py::split_documents`

April to May and September to October for birds, which is what most visitors come for. Midsummer is pleasant and quiet. Winter is severe, the road floods more often, and the pub reduces to weekends only.

## Practical notes

Cash is still useful at the market and in smaller places, though cards are
accepted almost everywhere now. Mobile coverage is good in the centre and
patchy on the outskirts. The nearest full hospital is in Brightwater; there is
a minor injuries unit locally with limited hours.




**Chunk 4** — source: `guide_kestrelford.md#1` — produced by: `chunker.py::split_documents`

## Eat and drink

Four pubs, two cafés, and a bakery that sells out by 11am. The pubs serve food between 12 and 2 and again between 6 and 8:30, and outside those windows there is nowhere to eat at all. The bakery is the reason most people come back.

## What to see

The market square on a Saturday morning is the main event and has run continuously since the 1400s. The parish church has a 13th-century tower you can climb for £2. The old trackbed walk runs six miles to the next village along an easy gradient and is the best half-day here.

## Where to stay

Two inns on the square and a handful of rooms above the pubs. Booking ahead matters between May and September and not at all otherwise. There is no accommodation of any kind within four miles of the town in either direction.

## When to go




**Chunk 5** — source: `guide_pellew_sands.md#2` — produced by: `chunker.py::split_documents`

## When to go

June and September for the beach without the crowds. July and August are busy and the town is at its most itself, for better and worse. Winter is bleak, largely closed, and has a following among people who like that sort of thing.

## Practical notes

Cash is still useful at the market and in smaller places, though cards are
accepted almost everywhere now. Mobile coverage is good in the centre and
patchy on the outskirts. The nearest full hospital is in Brightwater; there is
a minor injuries unit locally with limited hours.




## Sample Answer

**Question:** What public transportation is available for getting around Brightwater?

**Answer:** For getting around Brightwater, there is a local bus that runs two routes on a 30-minute headway until 7 pm and stops entirely on Sundays, as well as taxis that must be phoned since they do not circulate looking for fares (`guide_brightwater.md`). Additionally, a shuttle meets the four busiest arrivals from the train station to the campus (`guide_brightwater.md`).

**Sources retrieved:** `guide_brightwater.md`, `guide_halden_bay.md`, `guide_kestrelford.md`, `guide_regional_transport.md`

**Best distance:** 0.302  
**Relevance cutoff:** 0.6

**My relevance cutoff:**

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. --> I chose a relevance cutoff of 0.6. My five in-scope questions had best distances ranging from 0.302 to 0.478, while my five out-of-scope questions ranged from 0.853 to 1.046. Since lower distances indicate closer matches, 0.6 falls between the two groups and allows the relevant questions through while rejecting the unrelated ones.

| Question | In corpus? | Best distance |
|---|---|---|
| What are some fun attractions to visit in Brightwater? | Yes | 0.471 |
| Where can visitors find affordable food in Brightwater? | Yes | 0.478 |
| Where should visitors stay in Brightwater for a riverside location? | Yes | 0.447 |
| What public transportation is available for getting around Brightwater? | Yes | 0.302 |
| When is a good time to visit Brightwater for good weather while avoiding the busiest period? | Yes | 0.356 |
| What is the capital of Mongolia? | No | 0.880 |
| How do I change the oil in a diesel engine? | No | 0.905 |
| Who won the 1994 World Cup? | No | 1.046 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.853 |
| How do I write a for loop in Rust? | No | 0.878 |

## How I Used AI

**1.** I asked AI to help me understand how to replace the starter chunker for the city guides corpus. It suggested splitting the guides around paragraph boundaries with a maximum size of about 1,000 characters instead of cutting the text at arbitrary character positions. I used this approach and tested the resulting chunks to make sure they contained enough context and complete thoughts.

**2.** I asked AI to help me interpret the retrieval distances from my test questions. It helped me compare the in-scope distances of 0.302–0.478 with the out-of-scope distances of 0.853–1.046. Based on that comparison, I kept the relevance cutoff at 0.6 because it fell between the two groups, and I tested it to confirm that the system accepted the relevant questions and refused the unrelated ones.


<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 4/5 | 4/5 | 4/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Sampled chunks contain a complete thought and enough context | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. Named source supports the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

**Criterion 1 — Retrieved chunk contains the answer**

File: `results/run_2026-09-29_2108_before_scored.md`  
Produced by: `run_eval.py::main`

For the question "Where can visitors find affordable food in Brightwater?", the retrieved sources included `guide_eating.md`, and the system answered:

> Based on the documents provided, visitors can find comparable food for about a third less than the riverside strip on Corry Lane, which is two streets inland (`guide_eating.md`).

The scorer marked 4 of the 5 test questions as passing in each run.

**Criterion 2 — Every answer names a source**

File: `results/run_2026-09-29_2108_before_scored.md`  
Produced by: `run_eval.py::main`

For the transportation question, the system produced:

> Public transportation for getting around Brightwater includes a local bus that runs two routes on a 30-minute headway until 7 pm and stops entirely on Sundays, as well as taxis that must be phoned since they do not circulate for fares (`guide_brightwater.md`).

All five answers named at least one source document.

**Criterion 3 — Gate stops out-of-corpus questions**

File: `results/run_2026-09-29_2108_before_scored.md`  
Produced by: `run_eval.py::check_out_of_scope`

The relevance gate produced:

> What is the capital of Mongolia? — best distance 0.880 — refused  
> How do I change the oil in a diesel engine? — best distance 0.905 — refused  
> Who won the 1994 World Cup? — best distance 1.046 — refused  
> What is the recommended dosage of ibuprofen for a headache? — best distance 0.853 — refused  
> How do I write a for loop in Rust? — best distance 0.878 — refused

The gate refused 5 of 5 out-of-scope questions.

**Criterion 4 — Sampled chunks contain a complete thought and enough context**

Output from: `python app.py chunks -n 5`  
Produced by: `chunker.py::split_documents`

One sampled chunk from `guide_kestrelford.md#1` contained:

> Four pubs, two cafés, and a bakery that sells out by 11am. The pubs serve food between 12 and 2 and again between 6 and 8:30, and outside those windows there is nowhere to eat at all.

The five sampled chunks contained readable sections with enough surrounding information to understand their main points without needing the next chunk.

**Criterion 5 — Named source supports the answer**

File: `results/run_2026-09-29_2108_before_scored.md`  
Produced by: `run_eval.py::main`

For the question "When is a good time to visit Brightwater for good weather while avoiding the busiest period?", the system answered:

> Late May is arguably the best time to visit Brightwater because the days are long, everything is running, and the students are gone.

It named `guide_seasons.md` as the source supporting the answer. The named sources supported the answers for all 5 test questions.

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | The target was at least 4 of 5 questions, and 4 of 5 passed in all three runs, so the target held consistently. |
| 2 | Every answer names a source | MET | The target was 5 of 5 answers naming at least one source, and all five answers named a source in all three runs. |
| 3 | Gate stops out-of-corpus questions | MET | The target was at least 4 of 5 out-of-scope questions being refused, and the relevance gate refused all 5 of 5. |
| 4 | Sampled chunks contain a complete thought and enough context | MET | The target was at least 4 of 5 sampled chunks, and all 5 sampled chunks contained understandable information and enough context to identify their main point. |
| 5 | Named source supports the answer | MET | The target was at least 4 of 5 questions, and the named sources supported the answers for all 5 questions in each run. |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->


None of my five criteria were missed. Each criterion met its original target across the three runs.

However, Criterion 1 had the closest result to its threshold. Its target was 4 of 5 questions, and it achieved exactly 4 of 5 in all three runs. Because the system only met the minimum target rather than exceeding it, I would tighten this criterion in a future evaluation from 4 of 5 to 5 of 5 questions. This would make the evaluation stricter and expose the remaining failure instead of allowing one question to fail.

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. --> 

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
