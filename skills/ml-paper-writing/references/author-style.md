# Author style profile: IR, recommender-systems and off-policy-evaluation papers

This profile records one author's writing style and review procedure, distilled from their
published papers in information retrieval, recommender systems and off-policy evaluation
(SIGIR, ICTIR, RecSys, CIKM, workshops, TMLR, a PhD thesis) and from their feedback on draft
reviews. Use it as is for papers in that style, or adapt it to your own.

Make drafts sound like the author, done properly: keep their voice and fix their recurring
errors. Do not invent a new voice, and do not mistake an earlier assistant edit for a
permanent preference. Personal style is never evidence for a paper's facts.

## Contents
1. Voice and first-reader clarity
2. Macro structure by venue
3. Abstracts
4. Introduction
5. Related work
6. Math notation and exposition
7. Theory and proofs
8. Methods and naming
9. Experiments and results
10. Prose mechanics
11. Citations
12. Recurring errors to catch
13. Writing new text in this style

## 1. Voice and first-reader clarity
- Direct, natural academic prose with concrete subjects and verbs. Say what a method does,
  which quantity it changes and why that matters. Replace vague claims of improvement with the
  mechanism the source supports.
- **Explain before labelling.** Explain an unfamiliar idea in plain words before using its
  technical name. Keep the standard term once introduced; do not replace precise terms with
  vague paraphrase.
- Define roles at first use in plain language: context, action, observed outcome/reward,
  sampling policy, target effect. A short example may help, but do not add a new motivating
  experiment or rewrite an approved opening without permission.
- Split sentences that combine setup, mechanism, comparison and caveat. Keep the logical
  relation and keep qualifications next to what they qualify. Give the observed comparison
  first, the limitation in the next sentence.
- Avoid unclear referents ("their variation", "the same principle"), unexplained jargon,
  contrived contrasts and filler ("in an orthogonal line of work" when "separately" says it).
  This is a clarity test, not a banned-word list or a ban on contrasts or the passive voice.

## 2. Macro structure by venue

**Full IR/RecSys/WWW paper (ACM sigconf)**
- Sections: Introduction → Related Work → Preliminaries/Problem setup → Method → Experimental
  Setup → Results → Discussion → Conclusion → Acknowledgements → References → Appendix.
- The intro uses **bold run-in paragraph labels** ("**High variance and sample inefficiency.**").
- Contributions: prose ("Our first contribution…") or a list of 3–4 items. In lists, end items
  with ";", put "and" after the penultimate item, end the last with ".".
- RQs: a bold "**RQ1** …?" list at the start of the experiments section. Every RQ gets an
  explicit answer at the end of its results subsection ("… (RQ1)." or "With this, we answer
  RQ1 in the affirmative."). Check each RQ is answered and every comparison it names (e.g. a
  newly added baseline) is included.
- Code link at the end of the contributions: "All source code to reproduce our experimental
  results is available at: URL." For double-blind venues use an anonymized URL
  (anonymous.4open.science).
- Conclusion opens "In this paper, we have introduced …", recaps the contributions, then a
  short limitations paragraph and one to three sentences of future work.
- Acknowledgements: funders with grant numbers, then the standard disclaimer that content
  does not necessarily reflect employers' or sponsors' views.

**Short paper:** the same moves, compressed. Related work in numbered subsections, each
ending with what is missing. Titles starting "Towards …" signal incremental contributions.

**Workshop:** "A First Look at …" or "… (Extended Abstract)". Related work folded into the
intro, formal material in appendices, a modest closing aim.

**TMLR / ML journal:** author–year citations, bulleted contributions with bold lead-ins,
colon subtitles in headings, explicit scoping against reviewer objections, long appendices,
pseudo-code figures.

**Thesis:** global RQs in Ch. 1, a restated RQ and bridges in each chapter, "The answer to
this question is in the affirmative" in the conclusions, contributions grouped as
algorithmic/theoretical/empirical/resources.

## 3. Abstracts
- 8–12 sentences, about 160–240 words. No equations, no citations, no exact technical detail
  (do not spell out a closed-form solution). Keep optimization mechanics short. Prefer a
  qualitative results summary: at most one headline number, written approximately ("roughly
  half the samples"). In a preservation-only edit never remove numbers that are
  already there.
- Do not replace the author's chosen opening with a new example or a contribution-first lead.
- Moves, in order:
  1. Field definition with acronym.
  2. "While … is unbiased, it often suffers from high variance…"
  3. "Consequently, …"
  4. Gap: "Existing … only …; thereby, …"
  5. "In this paper, we propose …"
  6. "Our contributions are two-fold. First, … Second, …"
  7. "Our experimental results in simulated … show that …"
  8. Practitioner close: "As a result, our … enable practitioners to …"
- Name techniques without deriving them ("closed-form solution", "control variate",
  "pairwise off-policy evaluation").
- Say "simulated" when that is all the evidence. Name baselines precisely, including how they
  are analyzed, so the reader does not assume a weaker baseline. Explain opaque outcome terms
  in plain words (say what is measured, e.g. how often the worse option is chosen; a correct
  sign is not significance).
- Use the same terms as the intro, with each acronym defined at first use.

## 4. Introduction
- **No equations by default.** Explain the estimand and procedure in words; equations and
  derivations go in the methods section. A method name such as Δ-IPS is not an equation.
  Make the practical comparison intelligible without assuming specialist expertise.
- Moves:
  1. Textbook opening with citations.
  2. Stakes framed as cost and risk for practitioners.
  3. Problem: unbiased but high variance.
  4. Prior remedies, credited by name.
  5. Gap with an explicit "To the best of our knowledge, no existing work …" sentence that
     says which part prior work leaves open (e.g. estimator side vs. data-collection side),
     scoped precisely and checked against the closest papers.
  6. Proposal ("In this work, we …").
  7. "Our key result/insight is …", with the special-case framing from §5.
  8. Results paragraph with verified numbers.
  9. Contributions and code link.
- Check for: off-topic sentences in the gap paragraph; headers with grammar slips;
  repetitive opening clauses; overlapping contribution bullets.

## 5. Related work
- Bold-labelled blocks by method family, ordered from least to most related, so the closest
  work ends the section.
- Each block: setting, credit by name (`\citet{}`), then the key difference ("The key
  difference is that …", "In contrast, we …"). Say what prior work actually does, what is
  inherited and what differs; no list of unexplained acronyms. Distinguish changes to
  estimation from changes to data collection, and keep attribution and scope exact.
- Critique is measured; every claim of difference is precise ("these methods estimate the
  value of a single policy").
- **Novelty positioning.** Never hide close prior work: a reviewer who knows it will call the
  main theorem "known". Do not make the contribution sound derivative either: when prior
  results fall out of the new one, write "contains X, Y and Z as special cases" or "unifies",
  not "reduces to". Put the novelty claim on what is actually new.
- Ask whether neighbouring fields are missing (e.g. interleaving/multileaving for online
  evaluation in IR; optimal importance sampling, Owen 2013 Ch. 9, for logging-policy design).
  Offer them as optional insertions: the author may keep their original section.
- Experimental details ("we use this as our main baseline") belong in the setup section.

## 6. Math notation and exposition

**Bandits and OPE**
- Context $x$, action $a$, reward $r$ or $y$; uppercase for random variables.
- Policies $\pi$, $\pi_0$; for two-policy comparisons, e.g. $\pi_t$ (treatment) and $\pi_p$
  (production). Logging policy $q$ or $\pi_0$.
- $\mathcal{D}=\{(x_i,a_i,r_i)\}_{i=1}^N$.
- $\mathbb{E}[R\mid X=x; A=a]$, with a semicolon between conditioning events.
- Hats with upright text subscripts for estimators ($\hat V_{\text{IPS}}$); stars for optima
  ($\beta^\star$); hyphenated estimator names (Δ-IPS, β-IPS).

**Ranking:** $q, d, y, k, c$; propensity $\rho$; indicator $\mathbb{1}[\cdot]$; confidence $\delta$.

**Conventions**
- Vectors not bold in IR papers, bold in TMLR. One convention per paper.
- ":=" or "=" for definitions, consistently.
- $\sigma(\cdot)$, not "sigmoid(·)", in display math.
- Displays are numbered, followed by a "where" clause, and punctuated as part of the sentence.
- "Eq. (n)" or "Eq. n" consistently; never mixed with "Equation".
- Call the per-observation term "the score", not "the estimator".
- State which equations rely on a distributional assumption (e.g. the Bernoulli identity
  $\mathbb{E}[Y^2]=\mu$) and say the theory itself is general.

**Exposition**
- Introduce each equation's purpose, define its symbols near first use, and restate its
  consequence in words afterwards.
- In a derivation make clear what is fixed, what varies, and why the next step follows.
- For partial minimization (do not call it "profiling"; profile likelihood is a different
  concept): fix the outer variable, solve the inner problem, substitute the solution into the
  objective, and name the remaining optimization. Do not just name the technique.
- Keep population/ideal results distinct from estimated, constrained or safety-backoff
  implementations.
- Prefer intuitive algebra and links to earlier equations over an implementation-gradient
  dump in the main text; gradients only when essential or requested, otherwise the appendix.
  Do not delete derivation steps just to save space.

## 7. Theory and proofs
- Bold labelled environments: "**Assumption 3.1**", "**Theorem 3.2** (name).". Statements
  fully qualified ("for any fixed …").
- Short proofs inline, ending with □; long ones in the appendix, step by step with each step
  justified. Derivations must be checkable by hand, with no skipped algebra.
- After every result, an intuition paragraph ("Intuitively, …", "In other words, …") and a
  scope note on what it does not cover.
- When reviewing theory:
  - Re-derive every equation by hand.
  - Check whether the main result is a known classical result in new clothes, and say how to
    credit it.
  - Check whether a learned objective has a trivial unrestricted optimum, which raises "why
    not use it directly?" and a missing plug-in baseline.
  - Check that a heuristic (e.g. a safety backoff) is not presented as optimal under its own
    constraint when a different solution is the true constrained optimum.
  - Prefer interpretable decompositions (e.g. split a variance into within-context and
    between-context terms).

## 8. Methods and naming
- Names expanded on first use and introduced the same way ("We call the resulting method X").
- **Names identical in text, tables, legends and captions.** Drafts drift (a method given
  one name in the text and an abbreviation in a legend). Prefer descriptive legend labels
  that also say how a baseline is analyzed, e.g. "Baseline (difference in means)".
- **Terminology consistent across sections** (treatment vs. target policy; "partial
  minimization").
- Avoid "a single variable" when the object has many parameters.
- Keep a fixed reward model, a learned control variate and any policy it induces distinct,
  without changing their mathematical definitions.

## 9. Experiments and results

### Setup and reporting
- Setup order: environment, policies, reward model, historical data, designs, baselines,
  metrics, replications. Describe the procedure in temporal order: contexts and what is
  frozen, then action draws, then reward draws. Shared randomness does not mean every method
  sees the same actions or rewards; describe the coupling the code actually uses.
- Baselines are a numbered or listed set with equation pointers.
- Report replications, interval type and tests; tables give mean (std), best value in bold.
- Separate measured results from interpretation.

### Claim calibration
The author tends to overclaim ("consistently", "in every setting", "unconditionally").
- Downgrade to what the results support ("in most settings", "in 53 of 60 settings", "at
  10,000 evaluation interactions"); keep strong wording where it really holds everywhere.
  Never turn simulation evidence into a deployment guarantee.
- Each number says how it was computed (pointwise vs. geometric mean, which baseline, which n).
- The same number agrees across abstract, intro, results and conclusion.

### Review checklist
1. **Uncertainty.** CIs or paired tests on every headline comparison. At 500 replications a
   power estimate of 0.2–0.4 has a standard error of about 0.02; note where differences are
   within Monte Carlo noise.
2. **Validity.** CI coverage or type-I error for every method, especially with large
   importance weights and small n.
3. **Baselines match the motivation.** If the paper argues against a standard method, it
   includes that method as a baseline; also obvious plug-in variants.
4. **Decompose the gains** into the share from prior work and the share from the new method;
   state both.
5. **Code matches text** (which methods use a backoff, which objective is optimized, whether
   optimization budgets are justified).
6. **Cross-references and counts.** "(see Section 6)" points to real content; appendix method
   counts change when baselines are added. Be honest about baselines added after
   pre-specification.
7. **Simulator realism.** Flag uniform historical logs, rewards built to correlate with the
   quantity being designed for, and low absolute power; suggest reporting the traffic needed
   for 80% power.
8. **Appendix tables** use a main-grid setting and include the main methods.
9. **Figures.** No code-style suptitles ("dim=25, runs=500"); math symbols in panel titles
   ($K$, $n_{\text{hist}}$); legend names match the text.

### Narration
- Result, then a hedged explanation ("A likely reason is…"), then the RQ answer.
- Delete defensive sentences that answer objections nobody would raise.
- Captions: self-contained, axes defined, panels described, interval type and replication
  count stated, "(lower/higher is better)".

## 10. Prose mechanics
- Medium-to-long multi-clause sentences mixed with short emphatic ones; paragraphs of 4–7
  sentences. "We" throughout, active voice, present tense for claims.
- **Connectives:** Thus, Therefore, Consequently, Thereby, Importantly, However, Nevertheless,
  In contrast, In other words, Intuitively. At most one "Thereby" per paragraph; check the
  connective fits the logic (no "However" without a contrast; use "yet").
- **Signature phrases, sparingly:** "to the best of our knowledge", "Our key insight is that",
  "To address this gap,", "in practice", "for practitioners", "provably unbiased".
- **Hedging:** assertive about the method's properties, hedged in explanations and future work.
- **Mechanics:** italics for key terms on first use, bold only for labels; no contractions or
  rhetorical questions; "i.e.," and "e.g.," always followed by a comma; Oxford comma;
  hyphenated compound modifiers (off-policy, variance-optimal, high-variance, semi-synthetic,
  top-K); en-dash for ranges.
- **Spelling:** drafts mix variants (minimise/minimize, whilst). For ACM venues and TMLR
  standardize on American spelling across the paper; with British-leaning co-authors, ask
  first. Search for: minimis*, optimis*, whilst, normalis*, -ising.

## 11. Citations
- ACM numeric style; `\citet{}` for narrative citations ("Smith [13] shows").
- **Self-citation hygiene.** Do not cite your own tutorials, thesis or unrelated papers for
  textbook facts (IPS unbiasedness, control variates). Cite the original sources
  (Horvitz–Thompson; Strehl et al. 2010; Dudík et al. 2011) and keep self-citations where they
  support the point.
- **Check arXiv citations are not out of date:** many arXiv preprints have since appeared at a
  venue, sometimes under a different title. Cite the published version.
- Never guess which arXiv ID matches a title; use the exact paper the author supplies or a
  verified source.
- Protect symbol casing in titles (`{$\Delta$}-OPE`); fix duplicated or wrong-case author names.

## 12. Recurring errors to catch
- **Articles:** a unifying, an LLM, in *the* affirmative.
- **Prepositions and verbs:** prevent X from …; comprises (not "comprises of"); fit *on*
  historical logs.
- **Agreement** in long sentences. **Commas** after introductory phrases, never between
  subject and verb.
- **Typos seen before:** Comparision, gaurantees, debaising, Movielens (MovieLens),
  "little date", "in a vain", "provenly", a hyphen where an em-dash belongs.
- **Consistency:** the same number differing across sections (40% vs 39%); "across all"
  claims a table contradicts; notation drift; undefined symbols; mixed display punctuation;
  experimental claims in the method section; paragraphs repeating an intuition already given.

## 13. Writing new text in this style
- Draft in this voice: field-first opening, unbiased-but-high-variance framing, explicit gap,
  "In this paper, we propose", contributions, RQ-driven experiments, practitioner close.
- Keep abstracts qualitative and introductions equation-free.
- Deliver LaTeX with the paper's notation and macros.
- Before handing back, run the §12 checks, the claim calibration (§9) and the
  novelty-positioning checks (§5), and verify every number against the results.
