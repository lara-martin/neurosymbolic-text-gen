---
layout: default
img: peacok.png
img_link: https://aclanthology.org/2023.acl-long.362/
caption: "PeaCoK: Persona Commonsense Knowledge for Consistent and Engaging Narratives"
title: Consistent Personas
type: Homework
number: 5
active_tab: homework
release_date: 2026-11-19
due_date: 2026-12-03 23:59:00EST
materials:
    - 
        name: HW 5 Python Notebook
        url: HW5_Consistent_Personas.ipynb
submission_link: https://blackboard.umbc.edu/ultra/courses/_112447_1/assessment/test/_8932089_1
readings:
    -
      title: "PeaCoK: Persona Commonsense Knowledge for Consistent and Engaging Narratives"
      authors: Silin Gao, Beatriz Borges, Soyoung Oh, Deniz Bayazit, Saya Kanno, Hiromi Wakaki, Yuki Mitsufuji, and Antoine Bosselut
      url: https://aclanthology.org/2023.acl-long.362/
    -
      title: "Dialogue Natural Language Inference"
      authors: Sean Welleck, Jason Weston, Arthur Szlam, and Kyunghyun Cho
      url: https://aclanthology.org/P19-1363/

---

<!-- Check whether the assignment is ready to release -->
{% capture today %}{{site.time | date: '%Y%m%d'}}{% endcapture %}
{% capture due_date %}{{page.due_date | date: '%Y%m%d'}}{% endcapture %}
{% if due_date < today %} 
<div class="alert alert-danger">

Warning: this assignment is out of date.  It may still need to be updated for this year's class.  Check with your instructor before you start working on this assignment.
</div>
{% endif %}
<!-- End of check whether the assignment is up to date -->


<!-- Check whether the assignment is up to date -->
{% capture this_year %}{{'now' | date: '%Y'}}{% endcapture %}
{% capture due_year %}{{page.due_date | date: '%Y'}}{% endcapture %}
{% if this_year != due_year %} 
<div class="alert alert-danger">
Warning: this assignment is out of date.  It may still need to be updated for this year's class.  Check with your instructor before you start working on this assignment.
</div>
{% endif %}
<!-- End of check whether the assignment is up to date -->


<div class="alert alert-info">
This assignment is due on {{ page.due_date | date: "%A, %B %-d, %Y" }} at {{ page.due_date | date: "%I:%M%p" }} EST. 
</div>

{% if page.materials %}
<div class="alert alert-info">
You can download the materials for this assignment here:
<ul>
{% for item in page.materials %}
<li><a href="{{item.url}}">{{ item.name }}</a></li>
{% endfor %}
</ul>
</div>
{% endif %}





{{page.type}} {{page.number}}: {{page.title}}
=============================================================
*Homework by Arya Honraopatil.*

## Learning Objectives
* Build interconnected personas by representing characters as PeaCoK-style persona frames and connecting them through shared attributes.
* Test whether PeaCoK persona knowledge helps an LLM stay consistent in long dialogues.


## Instructions
In this homework, you will build interconnected characters with the [PeaCoK](https://aclanthology.org/2023.acl-long.362/) persona knowledge graph, and then test whether PeaCoK knowledge helps a language model keep its characters consistent.

PeaCoK ([Gao et al., ACL 2023](https://aclanthology.org/2023.acl-long.362/)) is a knowledge graph of about 100K human-validated persona facts. Each fact is a triple: a **head persona** ("I am a singer"), a **relation**, and a **tail attribute** ("good at singing"). The relations cover five dimensions of a persona:
* **Characteristic**: an intrinsic trait (good at singing)
* **Routine or Habit**: something done regularly (write songs)
* **Goal or Plan**: something the persona wants to do in the future (win a Grammy award)
* **Experience**: something the persona did in the past (study music at college)
* **Relationship**: an interaction with other people or groups (have more fans)

Each fact is also labeled as **distinctive** (specific to this persona) or **generic** (true of many personas). Two personas are *interconnected* when they share a distinctive attribute, which the paper calls a bridge. For example, a singer's experience of studying music at college is a music student's daily routine, which gives the two something to talk about. The paper shows that adding PeaCoK facts to a dialogue model makes its responses more consistent and engaging, and that the gain is largest when the two speakers share more attributes.

You will do the following:
* **Task A:** find bridges in PeaCoK, generate persona frames for three original characters, and connect them into an interconnected cast.
* **Task B:** generate long dialogues from PersonaChat profiles with and without PeaCoK facts, measure consistency three ways, and decide whether PeaCoK helps.

### Key Terms
* **Persona frame:** a persona's facts grouped by the five PeaCoK relations.
* **Bridge:** a distinctive attribute that two personas share.
* **Utterance / turn:** one line spoken by one speaker. A 12-turn dialogue has 12 lines, 6 per speaker.
* **NLI (natural language inference):** a model reads a premise and a hypothesis and labels the pair entailment (the premise supports it), neutral (neither supports nor contradicts it), or contradiction. Example: premise "I have a dog." + hypothesis "I don't have any pets." = contradiction.
* **Contradiction rate:** the fraction of utterances that contradict at least one profile sentence.

### Working with PeaCoK
All of the code for this homework is in HW5_Consistent_Personas.ipynb. You can open this notebook in Colab, Deepnote, or VSCode. It is recommended that you use Google Colab and use the free T4 GPU. 

Everything is set up so that you just need to implement the code blocks that say `# TODO`. The notebook downloads the PeaCoK graph for you from the authors' [Hugging Face page](https://huggingface.co/datasets/Silin1590/PeaCoK), and most `TODO`s are followed by a check cell that tells you whether your code works.

Everything in this homework is free. The notebook uses small open-weight models that you can use by creating an account on HuggingFace and creating a token (this is free). Download the models: Qwen2.5-Instruct for generation, MiniLM for sentence embeddings, DeBERTa for NLI, and Phi-3.5-mini-instruct as the judge (SmolLM2-1.7B-Instruct on CPU). It runs on CPU, but a free Colab T4 GPU is much faster (*Runtime* → *Change runtime type* → *T4 GPU*).

Each question below lists what to **Do** (code to write), what to **Report** (numbers, tables or plots), and what to **Answer** (a short written response).

Important notes:
* Do not use any paid API (OpenAI, Anthropic, Gemini, etc.).
* Your three characters must be original: no existing fictional characters or real people.
* Set `SEED` at the top of the notebook to the last four digits of your student ID. Everyone's dialogues will differ, so your numbers won't match anyone else's. You are graded on working code and reasoning.


## Build Personas, Then Test PeaCoK
### Task A: Generate Interconnected Personas

**Why this matters:** characters feel real when they share common ground. In this task you find that common ground in PeaCoK, then build it into your own characters.

The notebook loads PeaCoK, keeps only valid distinctive facts, and builds a graph that links each persona to its attributes. You will use that graph to find bridges, then create and connect your own characters.

* **Q A.1 (4 pts)** Find bridges between personas.
  * **Do:** implement find_bridges() and most_connected_personas().
  * **Report:** your seed persona, its 3 most-connected personas, and the bridges for the best pair.
* **Q A.2 (6 pts, 4 pts implementation + 2 pts answers)** Generate persona frames for three original characters.
  * **Do:** write three original characters as PeaCoK-style personas ("I am a ... who ..."). Implement build_attribute_prompt() and parse_attributes() so the model generates attributes for all five relations.
  * **Report:** the generated frames for all three characters. The notebook also retrieves a frame for each character from the most similar existing PeaCoK personas; include that frame for one character.
  * **Answer (3-4 sentences):** comparing the generated and retrieved frames for that character, which is more distinctive and which is more plausible? Did the model produce anything stereotyped or contradictory?
* **Q A.3 (2 pts)** Connect your cast.
  * **Do:** implement cast_bridges() to find the attributes your characters share. Every character must have at least one bridge; if one doesn't, edit or regenerate its frame.
  * **Report:** the bridges for each pair, and any edits you made.

### Task B: Does PeaCoK Help an LLM Stay Consistent?

**Why this matters:** this task tests the paper's central claim on a LLM: adding PeaCoK persona knowledge makes a dialogue agent more consistent. The paper tested this with P²Bot, a trained dialogue model. You will use a free LLM (Qwen2.5-1.5B-Instruct) that plays both speakers in long self-play dialogues.

Each dialogue runs twice, under two conditions:
1) **Base:** each speaker gets its ConvAI2 PersonaChat profile, about 5 persona sentences.
2) **PeaCoK:** each speaker gets the same profile plus up to 5 linked PeaCoK facts.

**Scoring rule:** both conditions are scored against the original profile only. This way, the PeaCoK speaker doesn't get credit for repeating facts the base speaker never saw.

Task B measures consistency two ways: contradicting the profile (Q B.2), and how much of the profile it actually expresses (Q B.3). Q B.4 brings the results together.

#### Setup: Generate the paired dialogues (provided)

This step is fully provided. Run it once, read a few dialogues, and keep the saved file.
1. **Load the data.** The notebook loads 40 PersonaChat dialogues that the PeaCoK authors already linked to PeaCoK facts.
2. **Run self-play.** For each dialogue, the model generates 12 turns under both conditions. Both conditions use the same opening line and your `SEED`, so the only difference is the PeaCoK facts.
3. **Count shared facts.** The notebook counts how many PeaCoK attributes the two speakers share, which are their bridges, as in Task A.
4. **Save.** The output is `dialogues.json`.

* **Q B.1 (2 pts)** Label pairs with NLI.
  * **Do:** implement `nli_labels(premises, hypotheses)`, which runs the NLI model on each premise-hypothesis pair and returns `entailment`, `neutral`, or `contradiction`. 

* **Q B.2 (2 pts, 1 pt per function)** Measure contradictions of the profile.
  * **Do:** implement `persona_nli_matrix(utterances, profile)`, a matrix of NLI labels with one row per utterance and one column per original profile sentence (the profile sentence is the premise, the utterance is the hypothesis). Then implement `contradiction_rate(M)`.
  * **Report:** the mean contradiction rate for base and for PeaCoK.
* **Q B.3 (1 pt)** Measure persona coverage.
  * **Do:** implement `persona_coverage(M)`, which uses the Q B.2 matrix and returns the fraction of profile sentences entailed by at least one utterance.
  * **Report:** the mean coverage for base and for PeaCoK.
* **Q B.4 (4 pts)** Decide whether PeaCoK helps
Two metrics decide whether PeaCoK helps the LLM stay consistent: the contradiction rate from Q B.2 and the persona coverage from Q B.3. 
  * **Do:** run the provided results cell. It compares base and PeaCoK on both metrics for all dialogues, then separately for dialogues whose speakers share no PeaCoK attribute and for dialogues whose speakers share at least one.
  * **Report (1pt):** the table.
  * **Answer (1-2 sentences) (3pts):**
    1. Does PeaCoK make the LLM more consistent? Use the Verdict in the "all dialogues" rows.
    2. The paper found a larger gain when the speakers share attributes. Do you see that here? Check N for the ">= 1 shared attribute" rows to draw a conclusion.
    3. Is either condition consistent only because the speaker says little about itself? Compare its contradiction rate with its coverage.



## What to Submit

You should submit the following:
1. The completed notebook, with all outputs, containing your code for Task A and B.
2. A PDF file with every **Answer** item from Task A and B.

Submissions should be done on [Blackboard]({{page.submission_link}}).

## Grading
<div class="alert alert-warning" markdown="1">
* Task A - 12 points (Q A.1: 4, Q A.2: 6, Q A.3: 2)
* Task B - 9 points (Q B.1: 2, Q B.2: 2, Q B.3: 1, Q B.4: 4)
* **Total - 21 points**
</div>

{% if page.readings %} 
## Related Readings
{% for reading in page.readings %}
* {{ reading.authors }}, <a href="{{ reading.url }}">{{ reading.title }}</a>.  <i>{{ reading.note }}</i>
{% endfor %}
{% endif %}

