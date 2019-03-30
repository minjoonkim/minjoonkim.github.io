---
layout: post
title: Mind the Theoretical Gap&#58; HCI 연구에서 쓰이는 Behavioral Change Theory 정리 - Part 1
excerpt: "관심 연구주제에 대한 1차 정리. 내 관심 주제에 대한 HCI를 통한 behavior change 이다. HCI/UX 분야에서 자주 등장하는 behavioral change theory 등을 정리해보고자 하다가 이 논문을 발견, 읽는 중이다. 좋은 overview 논문인듯 하다. 논문 자체가 세부적인 예시를 들어가며 정리된 논문이라 이 논문 + 관련 논문을 보려면 꽤나 많은 논문들을 봐야할것으로 예상된다. 이 부분을 필두로 여러 포스팅에 걸쳐서 정리를 한번 해보고자 한다."
image:
  feature: https://d.pr/i/JQzDrk+
categories: [research, behavior change, hci]
comments: true
---

**논문제목: Mind the Theoretical Gap: Interpreting, Using, and Developing Behavioral Theory in HCI Research /CHI 2013**  
저자: _Hekler, Klasnja, Froehlich, et. al._

관심 연구주제에 대한 1차 정리. 내 관심 주제에 대한 HCI를 통한 behavior change. HCI/UX 분야에서 자주 등장하는 behavioral change theory 등을 정리해보고자 하다가 이 논문을 발견, 읽는 중이다. 좋은 overview 논문인듯 하다. 논문 자체가 세부적인 예시를 들어가며 정리된 논문이라 이 논문 + 관련 논문을 보려면 꽤나 많은 논문들을 봐야할것으로 예상된다. 이 부분을 필두로 여러 포스팅에 걸쳐서 정리를 한번 해보고자 한다.



## Goal of this Paper:

In HCI, more researchers are increasingly designing technologies to promote behavior change. A common stratetgy taken by researchers is to draw on theories from behavioral sciences to inform design. As such, this paper aims to provide HCI researchers with guidance on interpreting, using, and developing behavioral change theories by:
1. providing an overview of different forms of behavioral theory across levels of generality
2. discussing the current uses of behavioral theory in HCI based on the different level distinctions and highlight areas that have yet received much attention
3. enumerating a series of shortcomings of behavior theories as articulated within behavioral science itself,
4. suggesting ways HCI researchers can contribute to the development and refinement of behavioral theories



## Terminology

A common definition of behabioral theory proposed by Glanz and Rimer:
> “...a systematic way of understanding events or situations. It is a set of concepts, definitions, and propositions that explain or predict these events situations by illustrating the relationships between variables.”  

**Constructs:** fundamental components of a behavioral theory  
**Variables:** operational definitions of the constructs, particularly as they are defined in context  
**Design guidelines:** the principles formulated by HCI researchers to make behavioral theory and empirical findings actionable for designing behavior changes technologies  
**Behavior change technologies:** the broad array of systems and artifacts developed to foster and assist behavior chagne and sustainment



## Forms of Behavioral Theory
![](https://d.pr/i/0AWErk+)

#### Meta-models
: organizational structures of multiple levels of influence on individual behavior

examples: 
**social ecological model:** (in health-related behavioral science) identifies broad “levels” of inter-related associations and factors of influence on a behavior of interest.
 * micro-level factors such as genetics and biology,
* meso-level factors such as interpersonal relationships and, 
* macro-level factors such as urban design, public policy, and culture.

meta-models are valuable for identifying the “lens” a researcher is using and other “lenses” not currently emphasized by the researcher or the community at large.

By virtue of their generality, meta-models are typically short on specifics about determinants of behavior that could be used to directly inform the design of technical systems. Also, too often meta-models have too many levels of influence to adequately evaluate. _The use of meta-models in design requires a great deal of conceptual and formative work to translate into pragmatic design guideliness and system features_





#### Conceptual Frameworks

: describe relationships among the fundamental building blocks of a behavioral theory, constructs, and provide a more specific account of how constructs are inter-related. 

Conceptual frameworks encompass several commonly used theories, including: 
* Transtheoretical model [^1],
* Self-efficacy theory [^2],
* Theory of planned behavior [^3],
* Health belief model [^4], and
* Self-determination theory [^5]

From an HCI perspective, conceptual frameworks provide more specific guidance to the design and implementation of behavior change technologies. But, because of their emphasis on only one or two levels of analysis, conceptual frameworks _have the potential to disregard key factors that may be influencing a behavior_


#### Constructs

: the basic determinants or mechanisms that a theory postulates to influence behavior

examples:  
Social cognitive theory defines the notion of self-efficacy (a person’s assessment of his/her ability to perform certain behaviors in a particular context [^6])

In social cognitive theory, self-efficacy (construct), along with other constructs such as outcome expectancies are key determinant of behavior.

A common practice in the development of behavior change interventions is to selectively use constructs from one or more theories. _Although common, this practice makes it difficult to evaluate the utility of the entire conceptual framework as the entire framework was not tested._ This can lead to methodological flaws in interpreting the validity of behavioral theories.


#### Empirical Findings

: previously developed theories are insufficient to guide HCI research in some cases. In such cases, additional empirical work — often in the form of ethnographic and other qualitative approaches — can generate knowledge necessary to establish a starting point for design.

Empirical findings, by virtue of being observed in a given context, must be abstracted in some way to create generalized knowledge. Although it is tempting to directly generalize specific findings from empirical work, _such generalizations should be tempered by factors such as the target participant group, study length and size, and other relevant contexts._





다음 포스팅:  
Three broad uses of behavioral theory in HCI

1. to inform the design of technical systems
2. to guide evaluation strategies
3. to define target users

---
[^1]: Prochaska, J.O. and DiClemente, C.C. (1983). Stages and processes of self-change of smoking: toward an integrative model of change. J Consult Clin Psychol 51, 390–395. 
[^2]: Bandura, A.(1986). Social foundations of thought and action. Prentice Hall, Englewood Cliffs, NJ.
[^3]: Ajzen, I. (2002). Perceived Behavioral Control, Self‐Efficacy, Locus of Control, and the Theory of Planned Behavior. J Appl Soc Psych, 32, 665-683
[^4]: Becker, M. (1974). The health belief model and personal health behavior, J Healt Soc Behav, 18, 348-366.
[^5]: Deci, E.L. and Ryan, R.M. (1985) Intrinsic motivation and self-determination in human behavior. Plenum, New York, NY.
[^6]: Bandura, A. (1997). Self-Efficacy-The Exercise of Control. Worth Publishers, Inc. New York, NY.