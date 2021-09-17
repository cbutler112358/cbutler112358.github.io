---
title: "The Blobbian Biosphere"
date: 2021-08-15
permalink: /posts/2021/08/blog-post-9/
tags:
  - miscellaneous
---



<p>
In the game <a href="https://www.agar.io" target="_blank"  rel="noopener noreferrer">agar.io</a>, you
navigate a circular blob in an environment populated by nutrients and other players. Consuming
either of these increases the mass of your blob. The object of the game is to consume enough
to become the largest blob. Although simple, the game exploded in popularity following its
release. Ever since I first played this game, I've thought about programming my own version of it.
As I entered university, the desire to develop my own game morphed into a desire to
simulate it. Are there optimal strategies that players can follow? Is it better to play aggressive or 
passive? Should a player focus more time on hunting other players or consuming the specks of food
that litter the landscape? 
I was resolved on spending the few weeks I had in Maine this summer tackling this 
interest. I am fascinated by genetic algorithms and thought it would be good idea to marry
the two in one project. The most natural choice of language
was NetLogo, given its simple syntax and the plethora of existing programs I have
in the language. As I've mentioned in the past, NetLogo is a language I lean on the most since
agent-based simulations are an absolute joy to program and study!
</p>

<p>
Obviously, I wasn't interested in making my own game. I was much more interested in what kind of strategies
evolve when you give a bunch of simulated organisms a set of rules to follow. Since I wanted some sort of 
natural selection to take place, there had to be genetics. A blob's genome would determine how it behaves.
But what kind of behavior would that be
As soon as I undertook making my own version of Agar.io, I made a few changes... The most important
difference between the original version and my program is that my version is not a game! This means that 
the behavior of the blobs needed to be predetermined and not dependent

For one, the blobs 
aren't controlled by players, and so their behavior must be completely determined by predetermined
settings. Broadly, these behaviors include hunting, foraging, chasing, running, and breeding. The 
final behavior listed, breeding, leads into a second important difference: in my version, the blobs
``breed.'' I want to explore the most optimal strategies when environment conditions change, and the most
natural way of doing this is allowing blobs to breed and pass on their traits. 
</p>

<p>
Before a blob makes any decision, it looks around for a predator blob. Predatory blobs are determined by their
<i>fang size</i>. A blob is only capable of eating another blob if it's fang size is greater than the size of it's
prey. For example, a blob with a fang size of 4 can consume blobs of sizes 1, 2, and 3. However, larger fangs
are more expensive to maintain. If a blob spots a predator blob (any blob with a fang size greater than their
size), it will flee in the opposite direction. 
</p>

<p>
Blob size determines blob speed. Larger blobs will not be able to move as fast as smaller blobs, but the exact 
speed that each blob is capable of moving is a continuous variable. 
</p>

<p>
The blobs operate according to a simple, sequential set of rules that depends on their current energy, represented 
by an integer. The number attached to each blob is this quantity. Each blob also possesses a 
<i>maximum energy</i>. If the current energy of a blob surpasses it's maximum energy, it will search for 
another blob in some radius satisfying the same criterion to sexually reproduce. Sexual reproduction, in this 
case, is the production of 3 offspring with each trait inherited from either parent with equal probability. 
Parental inheritance can change based on some mutation probability. If mutation occurs, the value of the
inherited trait is assigned any other possible value completely randomly. Offspring
are disseminated randomly across the landscape. Following breeding, the parents die. 
</p>

<p>
If the current energy of the blob does not surpass it's maximum energy, then it will forage or hunt according
to some probability. Foraging is just as it sounds: the blob will look around for food and, if there is food, it 
will 
</p>

<p>
At the simulation outset, we see a smattering of colors representing the different sizes of the randomly
generated blobs. To encourage convergence to a suitable set of blobbian traits, the mutation probability is set
high at the beginning (9%) and then slowly reduced to 2% over the course of a few hundred time steps. 
The population is given the opportunity to explore a wide breadth of the genotype space.
This process is similar to <b>simulated annealing</b>. Once the mutation probability settles, the conditions of
the environment impose a bottleneck on the population, culling a majority of the blobs. The few that remain 
are only able to do so because they've found a sufficient genotype. These blobs will repopulate the landscape, often
to its full capacity. 
</p>

<p>
At capacity, however, the system is not stable. Fluctuations occur
as genotypes <b>vie</b> for control. Depending on environmental conditions, it is not uncommon to see 
blue and green blobs repopulate the landscape. If food is scarce, purple blobs will survive the bottleneck
as their greater speed allows for more efficient foraging. The blobs immediately following the 
bottleneck will likely be foragers. As the landscape is repopulated,  mutations often introduce the larger 
species back into the environment. The orange and red species may forage like their <b>conspeciates</b>,
but they may also evolve fangs to prey on the more abundant smaller species. Their greater size allows for 
greater longevity... In almost all cases, predators persist at a much smaller population size relative 
to the foragers. 
</p>


<figure>
    <img src='/images/vanilla_blobs.gif' alt='Sim config' height='750' width='750' class='center'/>
    <figcaption><b>Figure 1.</b> A description. </figcaption>
</figure>

<p>
Fascinating pheonmena arise from this simulation. Reducing the benefit of food consumption
favors the evolution of predation. When food is rare or the energy gained by its consumption is
low, purple blobs populate the landscape. Eventually, a mutation introduces a blob with fans allowed it
to consume other blobs. The number of predators depends strongly on the price paid for evolving
fangs.
</p>

<p>
Although possessing a large size comes with more energy and therefore a longer lifespan on average,
maintaining that size costs energy. Movement also costs energy 
</p>


<p>
Blob genotypes possess other characteristics I've yet to mention..
</p>

<p>
Now that we're familiar with the basic rules of this blobbian world, how do they <q>evolve</q> as time goes 
on? One of the easiest features we can study is the size of the blobs, indicated by their color. The 
first variable we can look at changing is the probability of food in the environment. As food becomes
scarce, we can make an educated guess that the larger species are less successful and are out-competed by
smaller and faster blobs. These blobs are more successful than the larger ones in navigating uncertain 
landscapes, but pay the price in the form of lower energy. As the food in the environment becomes more 
plentiful, will the large blobs make a comeback or remain at small numbers? Figure 2 shows the results of 
this experiment. Each data point is the average population for that color of blob out of 50 simulations. 
Only simulations that survived beyond 1000 time steps were kept. 
</p>

<figure>
    <img src='/images/color_selection.png' alt='Sim config' height='750' width='750' class='center'  align='right'/>
    <figcaption><b>Figure 2.</b> Average blob color (and thus size) for simulations surviving more than 
    1000 time steps. </figcaption>
</figure>

<p>
While I'm sure other metrics are more useful for visualizing the direction of evolution of the organisms within the 
simulation, storing the average number of blobs over the course of a simulation is the easiest to measure,
and communicates the selection of other important features correlated with blob size, such as speed and energy.
The parameters used to generate the simulation in Figure 1 are as follows:
</p>

<p>
Blobs are only able to survive for long enough when the food probability reaches about 0.6%. In this harsh
environment, there doesn't seem to be any clear advantage to a larger or smaller size. Larger blobs survive long
enough because of their larger energy pools, while small blobs benefit from speedy searching strategies. Either
size seems only able to take advantage long enough to breed, but not enough to maintain an appreciable average population.
When food probability passes 1%, the green blobs burst onto the scene, indicating a clear advantage to size.
Competition increases as the food probability ticks higher, with orange and blue blobs exercising their 
might. By 1.7% food availability, blue blob performance plateaus in favor of a orange and green duel. Eventually,
orange blobs prove superior at thriving in environments with food probability above 2%. 
</p>

<p>
Either extreme on the size spectrum performed rather poorly across the scenarios tested. The large red blobs
never surpassed 15 blobs per time step on average throughout the simulation. As food becomes more abundant,
blobs become more plentiful and make it difficult for the slower blobs to keep up. I suspect that the red
blobs took advantage of this and evolved fangs to prey on other blobs. On the other end of the size spectrum,
however, the purple blobs did even worse. While purple blobs are the fastest of all blob species, they have
the lowest energy. This means that they must constantly search for food in order to breed. As soon
as other blobs became more prevalent across the landscape, the purple blobs are easily elbowed due to their
struct resource requirement. 
</p>

<p>
What conditions might give rise to the selection of larger blobs? In the previous simulations, the movement 
cost was set to 0.1, so blobs could greedily navigate the landscape without incurring much of an energy 
cost (unless you're purple). For example, moving 8 steps would only cost 0.8 energy.
Increasing the movement cost to 1.0 would select against this strategy. This scenario
may arise naturally as a result of perilous climate, in which movement is strenuous. Another environmental characteristic
contributing to the selection of large blobs is the cost of maintaining a large body. Recall that larger
blobs must expend energy each time step in order to maintain having such a large mass! What happens to the 
blob population as this size cost parameter is varied in combination with the aforementioned change to the
movement cost? Figure 3...
</p>



<h2> References </h2>

[1] Finkbeiner, S.D, Salazar, P.A., Nogales, S., Rush, C.E., Briscoe, A.D., Hill, R.I., 
Kronforst, M.R., Willmott, K.R., & S.P. Mullen. Frequency Dependence Shapes the Adaptive Landscape 
of Imperfect Batesian Mimicry. <em>Proceedings of the Royal Society B</em>. 2018; 285. 

