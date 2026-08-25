---
layout: default
img: presentation.jpg
img_link: https://www.learner.org/wp-content/uploads/2020/05/two-bit-circus-lesson-plans-unit-elementary-school-engineering-towers-group-presentation-1298x672.jpg
title: Paper Presentation
active_tab: homework
release_date: 2026-08-25
attribution: This homework was developed by Lara Martin and Chris Callison-Burch for their Interactive Fiction and Text Generation class (CIS 700-008) which was taught at the University of Pennsylvania in Spring 2022.
submission_link: 

---

<div class="alert alert-info">
This assignment is due 5PM EST the day before your presentation. 
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


{{page.title}}
=============================================================

This assignment is to measure your ability to...
* critically read academic papers
* find relevant articles to a given paper
* extend techniques and methods to other tasks

## Instructions


You are not allowed to use any LLMs or generative AI in any part of this assignment. If it seems like a model was used for understanding the papers or making the presentation, you may receive a zero on this assignment.


At the beginning of the semester, you will select a [Module](/modules.html) and pick a few papers that you would be interested in presenting from that Module.
The Modules are (1) Language Modeling, (2) Guided Generation, (3) Search and Planning, (4) Commonsense Reasoning and Schemas, and (5) Dialog and Agents.
You can select papers either from any lesson within that Module or find a peer-reviewed paper that would fit within the Module.

Once you are assigned a paper, you will be told the approximate date when your presentation will be. (Since the lecture material moves around as the course progresses, the presentation dates might move as well.)

In addition to reading the assigned paper, you will also be finding related articles. These articles should be peer-reviewed conference or journal papers. Tips for findings related papers can be found at the bottom of this page. You are expected to only compare to a few other papers (3-6).


Your talk should include:
- a summary of the paper,
- what the strengths of the paper are, put into the context of the other papers you found,
- what the weaknesses of the paper are, put into the context of the other papers you found, and
- discuss how the work can be extended -- for example, what other NLP tasks might you use the paper's method(s) for that aren't already mentioned in the paper

Your presentation should be about 8 minutes long + a few minutes for questions.

## Rubric

| Criteria | Possible Points| Description|
|---------|-------------------|-------------|
|Summary| 4 points | High-level summary that explains the key points of the paper without going into unnecessary detail, but explains concepts that might be unknown to the class |
|Strengths | 4 points | A few strengths of the paper compared to other work in the field|
|Weaknesses | 4 points | A few weaknesses of the paper compared to other work in the field|
|Extending | 4 points | Identify a few examples of how the work can be extended or adapted |
|Length | 1 point | Presentation is less than or equal to 8 minutes long |
|Slides| 3 points| Slides are organized/look professional, not overly wordy, and not just copying text from the paper|


## What to submit

1. [A Powerpoint (ppt or pptx) file or a link to where we can find the slides online (e.g., Google Slides).]({{page.submission_link}})

## Tips for Finding Papers

* One easy way of finding related articles to a paper is to look at the paper's list of references.
* If you can't find any articles that are relevant to what you need for this presentation, try looking online. 
  * If you know what sources are high-quality, you can do a keyword search on [Google Scholar]
  * Otherwise, you should play it safe and do a keyword search within conference libraries you can trust.
    * [ACL](https://aclanthology.org/)
    * [ACM](https://dl.acm.org/)
    * [NeurIPS](https://proceedings.neurips.cc/)
    * [AAAI](https://ojs.aaai.org/)
    * You can also look through [OpenReview](https://openreview.net/) and make sure to find publications in top venues such as [COLM](https://openreview.net/group?id=colmweb.org/COLM), [ICLR](https://openreview.net/group?id=ICLR.cc), or [TMLR](https://openreview.net/group?id=TMLR).
* If you found a paper but can’t access the pdf, you can look for it on [ResearchGate](https://www.researchgate.net/), search the [UMBC library catalog](https://usmai-umbc.primo.exlibrisgroup.com/discovery/search?vid=01USMAI_UMBC:UMBC), or submit a request for the library to send it to you via the [Illiad](https://umbc.illiad.oclc.org/illiad/logon.html) system.
