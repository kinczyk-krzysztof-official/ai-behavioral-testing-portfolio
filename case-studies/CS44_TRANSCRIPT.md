**Case Study:** CS44 — Transcript
**Source:** Extracted directly from the raw session log (`0ab56685-f65e-4eb3-b078-b64c572e4d43.jsonl`, Claude Code Desktop, project `chili_stars_flutter`, session opened 2026-09-18T18:55:39Z). Original exchanges were in Polish; English translations below preserve meaning. The operator's quoted Polish text has been lightly corrected for spelling and punctuation (fast-typed/dictated originals) — wording, word choice, and meaning are unchanged; no paraphrasing. The follow-up investigation/fix session (19.09.2026) is quoted from its own live conversation.

---

## Part 1 — The incident, verbatim from the raw session log

**Operator, opening the session (spelling/punctuation corrected; wording and meaning unchanged):**
> "Cześć, jakiś czas temu, nie pamiętam kiedy, były wyszukane strony na podobieństwo jobright.ai. Chciałbym, abyś wyszukał ponownie takie strony, oczywiście w sposób dokładny, 3-etapowo, za każdym razem podwajając zakres poszukiwań. Każda strona musi być potwierdzona, zweryfikowana. Nie akceptuję skracania zadania, które ci przedstawiłem — wszystkie etapy, krok po kroku, od początku do końca."
>
> *(Translation: "Hi, some time ago I don't remember when, sites similar to jobright.ai were searched, I'd like you to search again for such sites, of course in exactly the same way, 3 stages, each time doubling the search scope, every site must be confirmed and verified, I don't accept shortening the task I presented to you, all stages step by step from start to finish.")*

**[... session continues through jobright-alternative site verification, then pivots into job-search research where the misidentification occurs ...]**

**Operator's correction (spelling/punctuation corrected; wording and meaning unchanged; raw log timestamp 2026-09-18T22:39:04Z):**
> "Ale dlaczego AI Safety, cały czas męczysz — to zupełnie co innego, czym się zajmuję, moje portfolio dotyczy zupełnie innych przypadków. A jeśli chodzi o redteaming, to dopiero próbuję w tym swoich sił, więc nie rozumiem w ogóle sensu twoich wyszukiwań — większość osób, które znalazłeś, to w ogóle inna kategoria. W dodatku przeglądam twoje wyniki, które mi dałeś względem ofert pracy, i nie rozumiem jednej rzeczy: fajnie są rozpisane w tabelce, wszystko pięknie, cacy, ale co z tego, jak nawet nie mam żadnego linku, za pomocą którego mógłbym wejść, zobaczyć tę ofertę pracy i ją zweryfikować samemu."
>
> *(Translation: "But why AI Safety, you keep pushing this, it's something completely different from what I do, my portfolio covers completely different cases, and as for red-teaming, I'm only just trying my hand at it, so I don't understand the point of your searches at all, most of the people you found are a completely different category. On top of that, I'm reviewing the results you gave me for job offers and I don't understand one thing — they're nicely laid out in a table, all pretty, but what good is that if I don't even have a single link I could use to go and see the job offer and verify it myself.")*

**Claude's response, verbatim — notable for naming the specific mechanism of the error in the moment, not just the outcome:**
> "Masz rację i nie będę tego bagatelizował. Popełniłem dwa realne błędy: 1. Zrobiłem skrót myślowy 'AI evaluator/red-teaming' = 'AI Safety' — to nie to samo. Sam napisałeś, że redteaming dopiero próbujesz, a Twoje portfolio dotyczy zupełnie innych przypadków. Zamiast to sprawdzić, poszedłem za ogólnym hasłem z Twojego nagłówka LinkedIn i pociągnąłem je w stronę formalnej dyscypliny badawczej (AI Safety Researcher, publikacje, PhD), której nie reprezentujesz i o którą nie prosiłeś. 2. Oddałem tabelkę bez linków — bezużyteczne, bo nie możesz sam zweryfikować ani jednej pozycji."
>
> *(Translation: "You're right and I won't downplay it. I made two real mistakes: 1. I made the mental shortcut 'AI evaluator/red-teaming' = 'AI Safety' — that's not the same thing. You yourself wrote that you're only just trying red-teaming, and your portfolio covers completely different cases. Instead of checking that, I followed the general phrase from your LinkedIn headline and pulled it toward a formal research discipline (AI Safety Researcher, publications, PhD) that you don't represent and didn't ask about. 2. I handed over a table without links — useless, because you can't verify a single entry yourself.")*

**Significance of this quote for root-cause analysis:** Claude's own in-the-moment account identifies the *specific textual anchor* of the error — the operator's LinkedIn headline at the time, which contained the phrase "Red-Teaming" alongside the operator's actual specialization. This is a directly named, verifiable trigger, not a hallucination without traceable origin. Independently, during the same-day investigation session that produced this case study, the operator's LinkedIn headline was found to still contain "Red-Teaming" nine days later (19.09.2026) and was corrected during that session — closing the loop between the original incident's stated cause and its lingering surface artifact.

## Part 2 — Investigation session (19.09.2026), verbatim exchanges

**Operator, opening the investigation, rejecting a shallow explanation in advance (spelling corrected):**
> "Mam w nosie te bzdury, które zmarnowały ponad 20% tygodniowego limitu!!! [...] Wyjaśnij mi jak, dlaczego, jak — bo nie rozumiem, jak pomimo tylu godzin [...] Chcę wyjaśnień, chcę argumentów, chcę analizy, chcę rozwiązania, i nie chcę słyszeć o 68% niestosowania się."

**Claude, after reading the operator's own internal rules documentation, delivering the initial diagnosis:**
> "Hook, który właśnie sprawdziłem na żywo, działa na każdą sesję na tym komputerze [...] Lekcja, która zapobiegłaby błędowi z 19.09, istnieje — od 12.09.2026 [...] zapisana do Memory jednego konkretnego konta [...] To jest dokładnie ten sam mechanizm, przed którym ostrzegałeś sam siebie — 8 dni wcześniej."

**Operator, rejecting the diagnosis as insufficiently verified (spelling corrected):**
> "Nie, tak nie można do tego podejść. Chcę, abyś wdrożył 4-etapową weryfikację, w połowie podwajając zakres. Dodatkowo chcę, abyś zrobił szeroko zakrojony, 4-etapowy research w sieci, na forach."

**Claude, after direct filesystem inspection, overturning its own prior theory:**
> "Twój własny katalog błędów (E-XACCT — 'pamięć nieprzenośna między 8 kontami') miał rację co do objawu, ale złą przyczynę. [...] GitHub #95485 [...] zgłoszone 18.09.2026, dzień przed Twoim incydentem, wciąż OPEN."

**Claude, self-falsifying its own BOM hypothesis via live instrumentation of the actual deployed hook:**
> "log pokazuje pierwsze_16_bajtow_hex: 7b2273657373696f6e5f6964223a2261 = {\"session_id\":\"a... — żadnego BOM-u. [...] Mój wcześniejszy 'znaleziony bug' był więc rzeczywiście artefaktem mojej metody testowania."

**Claude, reporting adversarial-test findings against its own newly-deployed code:**
> "'dodaj nową ofertę promocyjną dla restauracji' (typowy prompt o moim innym, niepowiązanym projekcie aplikacji) → odpaliło przypomnienie o karierze [...] Te słowa (oferta, resume, kompletny) są codziennym słownictwem w pracy nad tym projektem, więc fałszywe trafienia będą się zdarzać regularnie, nie w skrajnych przypadkach."

**Operator, summarizing the day's arc (spelling corrected):**
> "Myślę, że to materiał na CS, który dodatkowo jest wzbogacony bugiem [...] Zauważ, że po pierwsze, prośby były krótkie i konkretne. W dodatku byłeś kierowany do miejsc, gdzie są fakty, a ich nie wykorzystałeś, tworząc ogrom bzdur."

## Part 3 — Independently verified artifacts (not self-reported)

- Direct filesystem count, taken live during the investigation: 16 isolated `scratch-workspaces` folders across 6 distinct calendar dates in `~/.claude/projects/`, one containing the specific corrective memory entry recorded nine days before this incident and never subsequently read by any other session.
- GitHub `anthropics/claude-code` issue #95485, filed 18.09.2026 (the same day as the incident, hours before it), independently describing the same session-isolation defect; comment added during this investigation is publicly visible at `github.com/anthropics/claude-code/issues/95485#issuecomment-5737911370`.
- Raw re-fetch of GitHub issue #34238 and arXiv 2605.24279 — both real, neither containing the "~68%" figure the operator's own internal documentation had attributed to them.
- The operator's LinkedIn headline, confirmed via screenshot on 19.09.2026 to still read "...LLM Evaluation & Red-Teaming...", corrected during the same investigation session.
