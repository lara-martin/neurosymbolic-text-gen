---
title: CMSC 412/612 - Neurosymbolic and Text Generation - UMBC
layout: default
active_tab: main_page 
---




<!-- Display an alert about upcoming homework assignments -->
{% capture now %}{{'now' | date: '%s'}}{% endcapture %}
{% for page in site.pages %}
{% if page.release_date and page.due_date %}
{% capture release_date %}{{page.release_date | date: '%s'}}{% endcapture %}
{% capture due_date %}{{page.due_date | date: '%s'}}{% endcapture %}
{% if release_date < now and due_date >= now %}
{% if page.type == "in-class" %}
<!-- In class activity -->
<div class="alert alert-danger">
The in-class activity for {{ page.release_date | date: "%A %b %-d" }} will be to <a href="{{ site.baseurl }}/{{page.url}}">{{ page.title }}</a>.  
</div>
<!-- Other participation activity -->
{% elsif page.type == "participation" %}
<div class="alert alert-info">
The participation activity <a href="{{ site.baseurl }}/{{page.url}}">{{ page.title }}</a> is due on {{ page.due_date | date: "%A, %B %-d, %Y" }} before {{ page.due_date | date: "%I:%M%p" }}. 
</div>
{% else %}
<!-- Homework assignment -->
<div class="alert alert-success">
<a href="{{ site.baseurl }}/{{page.url}}">{{page.type}} {{page.number}}: {{page.title}}</a> has been released.  
{% if page.deliverables %}
The assignment has multiple deliverables.
<ul>
{% for deliverable in page.deliverables %}
<li>{{ deliverable.due_date | date: "%b %-d, %Y" }} - {{deliverable.description}}.</li>
{% endfor %}
</ul>
{% else %}
It is due before {{ page.due_date | date: "%I:%M%p" }} on {{ page.due_date | date: "%A, %B %-d, %Y" }}.
{% endif %}
</div>
{% endif %}
{% endif %}
{% endif %}
{% endfor %}
<!-- End alert for upcoming homework assignments -->




# CMSC 412/612 - Neurosymbolic Text Generation at UMBC

## Fall 2026

### Prerequisites 
CMSC 341 and one of (CMPE 320, STAT 355, or STAT 451) with a grade of ‘C’ or better.


### Course Description
Pretrained language models (like LLMs) have the ability to generate coherent text that is far better than what previous generations of text generation models could produce. As a result, such models can be incredibly useful, but there are still a lot of unanswered questions surrounding them. Can they be safer? Solve complex problems? Tell stories? Neurosymbolic methods combine neural techniques (like LLMs or other neural networks) with older, symbolic AI techniques that are more interpretable and predictable in their behavior. In this course, we will be using and creating neurosymbolic methods as the "best of both worlds", namely improving LLMs by integrating symbolic methods such as knowledge graphs, rule-based engines, or planning. You will learn about various neural and symbolic techniques separately and how they can be incorporated together, developing your skills in natural language processing and cognitive modeling.

### Learning Objectives
By the end of the course, you will be able to...
<ol>
<li>Understand the strengths and weaknesses of neural language models (LMs) by themselves.</li>
<li>Implement and appraise the value of
	<ul>
	<li>conditioned generation,</li>
	<li>planning, and</li>
	<li>schemata</li>
	</ul>
	in text generation.</li>
<li>Discuss complex neurosymbolic systems and argue for the appropriate components of a working neurosymbolic text generation system.</li>
<li>Create your own neurosymbolic text generation system.</li>
</ol>





### Staff
**Instructor**
: [Lara J. Martin](https://laramartin.net)
: [laramar@umbc.edu](mailto:laramar@umbc.edu)

**TA**
: []()
: [](mailto:)

**Office Hours**
: Lara - Tuesdays from 3:15-5pm in ITE 342A or [by appointment](https://calendly.com/laramar/schedule)
: - <!--Wednesdays from 2-4pm in ITE 340 or [by appointment](mailto:dta1@umbc.edu)-->

### Logistics
**Time and Place**
: Fall 2026, Tuesdays & Thursdays from 11:30am - 12:45pm ET in Janet & Walter Sondheim 108
: First day of class is August 25, 2026
: Last day of class is December 8, 2026
: <!--Final project presentations will be held on December 11th from 10:30am - 12:30pm-->

### Course Materials
There is no textbook for this course, but you will be reading academic articles and book sections that will be provided to you. You may be required to purchase a variety of materials including software and API credits. If any of these are prohibitively expensive for your budget, please let the instructor know.

We will also be using Blackboard for assignment submissions & grades, and this course website will have an updated course schedule, readings, and instructions for the assignments.


#### Materials 
* [OpenAI API account](https://platform.openai.com/api-keys) - Pay-as-you-go
  * Pricing for each model can be found [here](https://platform.openai.com/docs/pricing).
  * Please **do not** sign up for the ChatGPT Plus subscription since you do not get access to the API with it.




### Grading

<table class="zui-table">
  <thead>
    <tr>
      <th>Assignment</th> 
      <th>412 (undergrad)</th>
      <th>612 (grad)</th>
    </tr>
  </thead>
  <tbody>
  <tr> <td>Homework 1</td> <td> 10% </td><td> 10% </td></tr>
  <tr> <td>Homework 2</td> <td> 10% </td><td> 10% </td></tr>
  <tr> <td>Homework 3</td> <td> 10% </td><td> 10% </td></tr>
  <tr> <td>Homework 4</td> <td> 10% </td><td> 10% </td></tr> 
  <tr> <td>Homework 5</td> <td> 10% </td><td> 10% </td></tr> 
  <tr> <td>Project</td> <td> 30% </td><td> 30% </td></tr>
  <tr> <td>Knowledge Checks</td> <td> 15% </td><td> 5% </td></tr>
  <tr> <td>Paper Presentation</td> <td> - </td><td> 10% </td></tr>
    </tbody>
</table>

### Assignment Descriptions
**Knowledge Checks**
: _Learning Objectives 1, 2, & 3_
: These checks are in place to see how well you all are understanding the material as the course goes. They will not be graded for accuracy, just whether or not you did them fully.  These might look like clicker questions (using Poll Everywhere), “minute” questions to get you to think about the topic of the day, or a small in-class assignment. There will be time devoted to doing them in class, but you are also allowed to make them up on your own time, including if you are not able to attend lecture. They will be posted either on Blackboard or the course website. Your two lowest grades (i.e., incomplete or missing submissions) will be dropped.

**Paper Presentations (Grad students only)**
: _Learning Objectives 2 & 3_
: Over the course of the semester, each graduate student must prepare one 5-minute presentation on a research paper relevant to the course. Since these presentation will be a substantial component of the learning experience in the class, slides must be prepared and emailed to the instructor & TA by 3PM the day before the presentation date.

**Homework 1-5**
: _Learning Objectives 1 & 2_
: There is one homework corresponding to each Module of the course. Each homework will test your understanding of and allow you to experiment with a particular method for generating text.

**Project**
: _Learning Objectives 3 & 4_
: Throughout the entire semester, you will work in groups to develop your own text generation system. The project is a chance for you to delve into one (or several!) of the topics we have covered in class. You can choose between two directions: creating a novel interactive experience or answering a research question. The final deliverable will be either a **demo** or a **paper**, respectively, and a poster presentation. You will have multiple milestones to check in and make sure your team is making progress.
: If you are trying to decide between multiple project ideas, or if you’re struggling to come up with something, we highly encourage you to come to office hours and discuss it with Dr. Martin. She will be able to help you narrow down which ideas of yours are the most feasible & interesting. 


### Class Policies
#### Collaboration Policy
Unless otherwise noted, you ARE allowed to work in pairs (2 people) on the homework assignments and a group of 3-5 for the final project. However, you must do the knowledge checks and paper presentation on your own.

#### Late Day Policy 
Each student has five free "late days" to be used on homeworks.  Each homework can be submitted at most two days late.  If you are out of late days, then you will not be able to get credit for subsequent late assignments. One "day" is defined as anytime between 1 second and 24 hours after the homework deadline. The intent of the late day policy it to allow you to take extra time due to unforseen circumstances like illnesses or family emergencies, and for forseeable interruptions like on campus interviewing and religious holidays.  You do not need to ask permission to use your late days.  No additional late days are granted. **Late days only apply to the homeworks. They cannot be used on project deadlines or paper presentations.**

Knowledge checks can be made up at any time; no excuse is needed. There will be an assignment for each knowledge check on Blackboard where you can submit your answer or materials. You are strongly encouraged to complete these in a timely manner so that we are assessing your knowledge at an appropriate time in the semester.

#### Academic Integrity
If you are struggling because of the material or having difficulties completing the assignments on time, please [reach out to Dr. Martin](mailto:laramar@umbc.edu) rather than copying another student or looking up answers online. We can come up with a solution to help you out before you feel like you need to resort to cheating.

I care a lot about the students who take my classes, and that also means that I take cheating very seriously. Plagiarism or any sort of cheating is not tolerated in this class. All work submitted must be your own (or, if permitted, with partners---see [Collaboration Policy](#collaboration-policy). If you are allowed external sources on an assignment, please be sure to cite your source! This includes Large Language Models (LLMs): Please see [the next section](#generative-ai) for our policy specific to ChatGPT and other generative AI. Remember, reusing your own work from a different class is not permitted; this is self-plagiarism. If you are suspected of cheating, plagiarism, or other forms of academic dishonesty, your case will be brought to the attention of the Undergraduate Academic Conduct Committee or Graduate Council Grievance Committee and may result in an F in the course, depending on the Committee’s decision. **Your first offense will result in at least a 0 (zero) on the assignment.** If you would like more information on what constitutes as academic dishonesty, please consult [https://academicconduct.umbc.edu/](https://academicconduct.umbc.edu/).

#### Using LLMs or Generative AI
This course is centered around text generation, and we will be using GPT for a large portion of it. That said, any time that you use a large language model (LLM) for an assignment you must provide (1) the exact prompt that you used and (2) the original, unedited generation.

If you use LLMs for any other writing (e.g., the project paper), you must provide the prompt and the original generation, but you are also required to show where you edited the original generation. This applies to prose, code, or any form of content creation. Not disclosing is an academic integrity violation. If you do disclose, your answer may receive anywhere from 0 to full credit, depending on the extent of substantive edits, achievement of learning objectives, and overall circumvention of those objectives. Generative AI may **not** be used for the grad presentations in any way.

Use of AI/automatic tools for grammatical assistance (such as spell-checkers or Grammarly) or small-scale predictive text (e.g., next word prediction, tab completion) is okay. Provided the use of these tools does not change the substance of your work, use of these tools may be, but is not required to be, disclosed.


------
## UMBC School Policies

### Accessibility and Disability Accommodations, Guidance and Resources
Accommodations for students with disabilities are provided for all students with a qualified disability under the Americans with Disabilities Act (ADA & ADAAA) and Section 504 of the Rehabilitation Act who request and are eligible for accommodations. The Office of Student Disability Services (SDS) is the UMBC department designated to coordinate accommodations that creates equal access for students when barriers to participation exist in University courses, programs, or activities.

If you have a documented disability and need to request academic accommodations in your courses, please refer to the SDS website at sds.umbc.edu for registration information and office procedures.

SDS email: [disability@umbc.edu](mailto:disability@umbc.edu)

SDS phone: [410-455-2459](tel:410-455-2459)

If you will be using SDS approved accommodations in this class, please contact the instructor to discuss implementation of the accommodations. During remote instruction requirements due to COVID, communication and flexibility will be essential for success.

### Sexual Assault, Sexual Harassment, and Gender Based Violence and Discrimination
[UMBC Policy](https://ecr.umbc.edu/interim-policy-on-sex-discrimination-sex-based-harassment-and-sexual-misconduct-august-1-2024/)  in addition to federal and state law (to include Title IX) prohibits discrimination and harassment on the basis of sex, sexual orientation, and gender identity in University programs and activities. Any student who is impacted by sexual harassment, sexual assault, domestic violence, dating violence, stalking, sexual exploitation, gender discrimination, pregnancy discrimination, gender-based harassment, or related retaliation should contact the University’s Title IX Coordinator to make a report and/or access support and resources. The Title IX Coordinator can be reached at [ecr@umbc.edu](mailto:ecr@umbc.edu) or [410-455-1717](tel:410-455-1717).

You can access support and resources even if you do not want to take any further action. You will not be forced to file a formal complaint or police report. Please be aware that the University may take action on its own if essential to protect the safety of the community.

If you are interested in making a report, please use the [Online Reporting/Referral Form](https://umbc-advocate.symplicity.com/titleix_report/index.php/pid364290?).  Please note that, if you report anonymously, the University’s ability to respond will be limited.


**Notice that Faculty and Teaching Assistants are Mandated Reporters with Mandatory Reporting Obligations**

All faculty members and teaching assistants are considered Mandated Reporters, per UMBC’s [Interim Policy on Sex Discrimination, Sex-Based Harassment, and Sexual Misconduct](https://ecr.umbc.edu/interim-policy-on-sex-discrimination-sex-based-harassment-and-sexual-misconduct-august-1-2024/). Faculty and teaching assistants therefore required to report all known information regarding alleged conduct that may be a violation of the Policy to the Title IX Coordinator, even if a student discloses an experience that occurred before attending UMBC and/or an incident that only involves people not affiliated with UMBC.  Reports are required regardless of the amount of detail provided and even in instances where support has already been offered or received.

While faculty members want to encourage you to share information related to your life experiences through discussion and written work, students should understand that faculty are required to report past and present sexual harassment, sexual assault, domestic and dating violence, stalking, and gender discrimination that is shared with them to the Title IX Coordinator so that the University can inform students of their [rights, resources, and support](https://ecr.umbc.edu/resources-2/).  While you are encouraged to do so, you are not obligated to respond to outreach conducted as a result of a report to the Title IX Coordinator.

If you need to speak with someone in confidence, who does not have an obligation to report to the Title IX Coordinator, UMBC has a number of [Confidential Resources](https://ecr.umbc.edu/resources-3/) available to support you: 

[Retriever Integrated Health](https://health.umbc.edu/) (Main Campus): [410-455-2472](tel:410-455-2472); Monday – Friday 8:30 a.m. – 5 p.m.; For After-Hours Support, Call [988](tel:988).

[Center for Counseling and Well-Being](https://shadygrove.umd.edu/student-affairs/counseling-well-being) (Shady Grove Campus): [301-738-6273](tel:301-738-6273); Monday-Thursday 10:00a.m. – 7:00 p.m. and Friday 10:00 a.m. – 2:00 p.m. (virtual) [Online Appointment Request Form](https://shadygrove.titaniumhwc.com/)

Pastoral Counseling via [The Gathering Space for Spiritual Well-Being](https://i3b.umbc.edu/spaces/the-gathering-space-for-spiritual-well-being/): [410-455-6795](tel:410-455-6795); [i3b@umbc.edu](mailto:i3b@umbc.edu); Monday – Friday 8:00 a.m. – 10:00 p.m.

[Women, Gender, and Equity Center](https://womenscenter.umbc.edu/) (open to students of all genders): [410-455-2714](tel:410-455-2714); [womenscenter@umbc.edu](mailto:womenscenter@umbc.edu); Monday – Thursday 9:30 a.m. – 5:00 p.m. and Friday 10:00 a.m. – 4 p.m.

#### Other Resources

[Women’s Center](https://womenscenter.umbc.edu/) (open to students of all genders): [410-455-2714](tel:410-455-2714); [womenscenter@umbc.edu](mailto:womenscenter@umbc.edu); Monday – Thursday 9:30 a.m. – 5:00 p.m. and Friday 10:00 a.m. – 4 p.m.

[Shady Grove Student Resources](https://ecr.umbc.edu/shady-grove-title-ix-resources/), [Maryland Resources](https://ecr.umbc.edu/maryland-resources/), [National Resources](https://ecr.umbc.edu/national-resources/).

#### [Child Abuse and Neglect](https://ecr.umbc.edu/child-protection/)

Please note that Maryland law and [UMBC policy](https://education.umbc.edu/child-abuse-reporting-policy/) require that faculty report all disclosures or suspicions of child abuse or neglect to the Department of Social Services and/or the police even if the person who experienced the abuse or neglect is now over 18.

### [Pregnant and Parenting Students](https://www2.ed.gov/about/offices/list/ocr/docs/pregnancy.html)
UMBC’s [Interim Policy on Sex Discrimination, Sex-Based Harassment, and Sexual Misconduct](https://ecr.umbc.edu/interim-policy-on-sex-discrimination-sex-based-harassment-and-sexual-misconduct-august-1-2024/) expressly prohibits all forms of discrimination and harassment on the basis of sex, including pregnancy. Resources for pregnant, parenting and breastfeeding students are available through the University’s [Office of Equity and Civil Rights](https://ecr.umbc.edu/students/).  Pregnant and parenting students are encouraged to contact the Title IX Coordinator to discuss plans and ensure ongoing access to their academic program with respect to a leave of absence – returning following leave, or any other accommodation that may be needed related to pregnancy, childbirth, adoption, breastfeeding, and/or the early months of parenting.

In addition, students who are pregnant and have an impairment related to their pregnancy that qualifies as disability under the ADA may be entitled to accommodations through the [Office of Student Disability Services](https://sds.umbc.edu/accommodations/registering-with-sds/).

### Religious Observances & Accommodations
UMBC [Policy](https://ecr.umbc.edu/faith-based-and-religious-accommodations/) provides that students should not be penalized because of observances of their religious beliefs, and that students shall be given an opportunity, whenever feasible, to make up within a reasonable time any academic assignment that is missed due to individual participation in religious observances. It is the responsibility of the student to inform the instructor of any intended absences or requested modifications for religious observances in advance, and as early as possible. For questions or guidance regarding religious observances and accommodations, please contact the Office of Equity and Civil Rights at  [ecr@umbc.edu](mailto:ecr@umbc.edu).

### Hate, Bias, Discrimination and Harassment
UMBC values safety, cultural and ethnic diversity, social responsibility, lifelong learning, equity, and civic engagement.

Consistent with these principles, [UMBC Policy](https://ecr.umbc.edu/discrimination-and-bias/) prohibits discrimination and harassment in its educational programs and activities or with respect to employment terms and conditions based on race, creed, color, religion, sex, gender, pregnancy, ancestry, age, gender identity or expression, national origin, veterans status, marital status, sexual orientation, physical or mental disability, or genetic information.

Students (and faculty and staff) who experience discrimination, harassment, hate, or bias based upon a protected status or who have such matters reported to them should use the [online reporting/referral form](https://umbc-advocate.symplicity.com/titleix_report/index.php/pid954154?) to report discrimination, hate, or bias incidents. You may report incidents that happen to you anonymously. Please note that, if you report anonymously, the University’s ability to respond may be limited.
