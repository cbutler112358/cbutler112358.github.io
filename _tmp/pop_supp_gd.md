---
title: "Gene drives and population suppression"
date: 2023-06-11
permalink: /posts/2023/06/blog-post-13/
tags:
  - miscellaneous
---

<p>
While I have had this website for years, I shockingly realized that not one of my blog posts have been
related to my "professional" research. Most of my Ph.D. has been spent studying gene drives, or
genetic elements that bias their own inheritance in target populations [1]. By target populations, I mean
any <i>regional</i> pest species. 
The use of the word "regional" is important here, since we want to use our gene drive against a single target species in a single, spatially defined region. To clarify what a "pest species" is, Worner and Gevrey define one as [3]
</p>

<q>
an organism that damages crops, destroys products, transmits or causes disease, is annoying or in other ways conflicts with human needs or interests
</q>

<p>
The list of organisms that fit this definition is long. The pest I work on most frequently is the yellow fever mosquito, <i>Aedes aegypti</i>. A significant source of mortality and morbidity in humans, <i>Ae. aegypti</i> spreads a lot more than the virus responsible for yellow fever, but also those responsible for Zika, chikungunya, and dengue. Another pest species is the southern house mosquito, <i>Culex quinquefasciatus</i>. This mosquito is important in the area of conservation, <a href="https://www.civilbeat.org/2022/12/in-a-race-against-time-feds-ramp-up-efforts-to-save-hawaiis-endangered-forest-birds/" target="_blank"  rel="noopener noreferrer">especially in Hawaii</a>, where it has wreaked havoc against the local avifauna thanks to its role in transmitting the avian malarial parasite, among other harmful pathogens [2]. 
</p>

<p>
Broadly speaking, gene drives can be divided into two categorites: population replacement and population suppression. Population replacement essentially involves genetically <i>modifying</i> an entire target population. For example, a desirable modification in mosquitoes is making them immune to those diseases harmful to humans. A mosquito immune to the Zika virus will not transmit it to humans. Population suppression drives, on the other hand, are designed to suppress or eradicate target species. This is similar to existing control strategies that primarily rely on the use of insecticides. The difference, ideally, is that gene drives are particular and regionally contained to a single (target) species. Population suppression is typically easier to accomplish <b>in the lab</b> because genetically modifying an organism in a way that is harmful to that organism is easier to do than genetically modifying an organism in a way that is both desirable to human interests and is fit enough to replace a wild population. 
</p>

<p>
Population suppression can also be effective in answering the problems created by pest species. How do you curb the transmission of mosquito-borne diseases? Kill the mosquitoes! A secondary benefit of suppression is that many pest species of medical concern are also invasive, so their eradication <a href="https://mauiinvasive.org/2016/03/18/no-mosquitoes-in-hawaii/" target="_blank"  rel="noopener noreferrer">will help restore native ecologies and be of little negative consequence to other species</a>. In some scenarios, suppression is the most practical option, such as with our earlier example of <i>Cx. quinquefasciatus</i>. How could you genetically modify these mosquitoes in a way that protects the avifauna of Hawaii and other threatened islands? You could immunize them against the avian malaria parasite, but then there is still the issue of West Nile virus and various avian poxviruses, both vectored by the mosquito and harmful to birds [2]. On top of all this, <i>Cx. quinquefasciatus</i> is invasive, having been accidentally introduced to the island in the 1800s. Given the circumstances, eradication seems the most effective strategy. (In general, the question of population eradication is anything but a simple question and concerns important social and political matters beyond this represented here [4]; this example is meant to be more illustrative of scenarios amenable to suppression/eradication, and not to minimize the complex process involved in such a scenario.) Population suppression is not a straightforward matter, however. Pest species can be resilient, adaptable, and resistent to modern control strategies&#8212;partly the reason why gene drives have received so much attention. 
</p>

<p>
Population suppression gene drives also raise many interesting biological and mathematical questions (some of which I've pursured in my own research). But you don't have to take my word for it&#8212;that is what models are for! The following simple model was an afternoon idea to explore some of the rich dynamics in population suppression. The agent-based model below simulates a population of wild-type and transgenic (gene drive-bearing) organisms on a grid of cells. Each cell contains only a single individual at a time. Density-dependence is included, &agrave la <a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life" target="_blank"  rel="noopener noreferrer">Conway</a>, with the following rules:
</p>
<ol>
	<li>If the (Moore) neighborhood of a cell contains more than three organisms, the cell dies;</li>
	<li>If the (Moore) neighborhood of an unoccupied cell contains two organisms, a new organism is produced in that cell.</li>
</ol>
<p>
Time is discrete and, during each time step (henceforth referred to as "tick"), organism mortality occurs with a certain probability. The mortality probability of wild-type and gene drive-bearing organisms is denoted as $\mu_{wt}$ and $\mu_{gd}$, respectively. For now, we take $\mu_{wt} = \mu_{gd} = 0.5$, so that the average lifespan for each organism is 2 ticks. When an organism is born (i.e., a cell becomes occupied), the genotype of the newly occupied cell is determined from the two "parents" (the two neighboring occupied cells). Two wild-type parents produce a wild-type offspring, while a gene drive-bearing parent only produces gene drive-bearing offspring&#8212;owing to that "biased inheritance" business mentioned at the very beginning. A simulation ends if it reaches 2500 ticks, or if either the total or gene drive-bearing population goes extinct. Drive-bearing organisms incur fitness costs that affect their lifespan and fecundity. For now, we will assume there are no viability costs and keep the lifespans of each genotype the same. However, how does the fecundity of drive-bearing organisms affect performance? Let's take a look.
</p>

<p>
The program is coded entirely in NetLogo and the analysis is carried out in R. The population is seeded with a handful of wild-type individuals that are allowed to reach equilibrium for 50 ticks before a release of transgenic organisms occurs. The release ratio used, relative to the wild-type population at equilibrium, is 5%. 
</p>

<p>
Link to SIAM news article

Unlike most of the afternoon projects I post
on this site, I actually think I am well-acquainted 
</p>

<figure>
    <img src='/images/mourning_doves.jpg' alt='Sim config' height='750' width='750' class='center'/>
    <figcaption><b>A pair of mourning doves (<em>Zenaida macroura</em>).</b></figcaption>
</figure>

<br>

<h2>References</h2>

[1] Standardizing the def'n of gene drive

[2] Culex quinquefasciatus: status as a threat to island avifauna and options for genetic control

[3] Modelling global insect pest species assemblages to determine risk of invasion

[4] ERADICATION AND PEST MANAGEMENT by Judith Myers



[1] Kodric-Brown, A., and J. H. Brown (1984). Truth in Advertising: The Kinds of 
Traits Favored by Sexual Selection. <em>The American Naturalist</em>. 124(3); 309-23.

[2] Wolfenbarger, L. L. (1999). Red coloration of male northern cardinals correlates with 
mate quality and territory quality. <em>Behavioral Ecology</em>. 10(1); 80–90.

