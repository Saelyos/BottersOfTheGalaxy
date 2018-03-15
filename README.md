# Botters of the Galaxy


What a special contest it was! The diversity of possible strategies and the complex rules made it really hard to understand what could be the best way to make a strong AI.   

I’ll try here to describe how I managed to write an efficient AI and eventually win :)


## Special contest, special approach
I usually start coding quite early on the contest to have a game engine quickly and to be able to improve all sort of things during the contest.  
This time was different: I didn’t want to implement a strategy that would relieved to be inefficient and would make me restart from scratch. Moreover, the rules were really complex and I wanted to have time to understand them well.  

So, I spent the first days reading the referee to understand how the game works on the details, and trying to think about what could be the best strategy. I was also coding a basic engine to predict the creep’s damages if I had to farm.


## Strategy 
On Wednesday I start writing my first real AI. At first, I went for the “hero rush” to go to legend as it was the easiest strategy to implement. The hero rush consists on doing everything possible to kill the enemy’s heroes, even if it involves diving (e.g. go under the tower).  I was initially planning on moving to another strategy but I decided to keep it for several reasons: 
-	All the matchups are almost the same: I go in, that’s all!
-	I don’t need to handle a lot of corner cases, so I know that I won’t lose time correcting details, but I can focus on improving my AI.
-	The AI I had was already good even if there were a lot of things that could be improved
-	I was lazy to do another thing more complex :)  

So, I went for an Hulk + Deadpool composition and tried to improve it as much as I could. Because I often take damages from the units and the tower, my main goal was always to end the game as soon as possible.

## Opponent composition
I need to know the hero I’ll focus first and since some of them are more defensive or have more mobility than others, I had the following focus order: Doctor Strange > Valkyrie > Hulk > Deadpool > Ironman   
You will see later that I make distinctions if I’m against a melee composition or a ranged composition but that’s the only difference I do. I didn’t need to target specific opponents.

## Finite State Machine
My global strategy can be seen as a very simple FSM with 3 states:  
The initial one is Pushing, and as soon as my hulk is behind 300 ranged of the focused hero, I go to the Killing state and I will stay on it until the end of the game. If I am against a melee composition, I have one round of the Engaging state between the 2 others.  



#### Pushing
If the enemy is not coming I push the lane by killing the opponent units. 
Don’t underestimate units! Coming to the opponent tower with 4 units brings me a high potential damage output.  
The way I deal damage to the first 4 creeps is hard-coded to be sure that I last hit all of them and earn 140 golds if the enemy is not coming to me.

#### Engaging
Very basic: Hulk shields and Deadpool moves towards.  
I don’t have an engaging state against ranged comp because the turn I lose shielding, the enemy is usually too far to engage.

#### Killing
The way I play the skills to implement my strategy is quite logical:   
The 2 skills I use in priority are the stun ones (Bash from hulk and Wire from Deadpool). They allow me to deal a lot of damages to a defenseless target. Naturally I play the 2 skills one after each other to immobilize the target during 4 turns. The charge from Hulk is also very useful to gap close.  

Against melee compositions I use the explosive shied if my Hulk is being focused and the counter if Deadpool is taking damages. Before I use counter I also check that the hero I’m focusing is the closest enemy unity of Deadpool to maximize the chances of dealing damage back.  

If I have no skill to use, I’ll will perform an Attack to my target or Move_Attack if I’m already on range. Move attacking allows me to be closer to the target, which is useful: 
-	If the target runs away, I am closer so I can follow quickly.
-	For Deadpool skills: I have less chance to fail them.

## Items and potions:
On the first two turns I buy items with the best ratio damage/cost that I can afford.   
Keeping in mind that I want to end the game quickly, I only consider buying a potion if I have killed an enemy and if one of my heroes is going to die, in order not to lose time. With the initial golds of the pushing part and the golds of the kill I usually have enough to buy the best health potion.

## Aggro
_Contrary to MeanMax where I went late to sleep for the last day and was ineffective at that time, I decided to wake up early and see what I could improve in the last hours. My bot was at this moment ranked about 10th. Taking aggro into account was the last improvement that I found about one hour before the end of the contest._

Because the creeps and the towers always target the closest hero (when both hero are attacking enemy), by moving my hero with the maximum health closer to the enemy units than my other hero I make sure that he will be targeted. In this way the health of my 2 heroes will go down at the same speed, and I have a lot more chance to kill a hero before one of mine dies. Being the first to make the kill is extremely important since a high amount of golds is earned after a kill.

I had this idea when I was trying to improve the way I dived, but it turned out to be effective against all match ups and especially against double melees. My winrates against top players raised significantly to push me to 7th place before rerun and to a solid first place after!


## Conclusion
Honestly, when I woke up on Monday morning I was far from expecting to win, I was only focused on getting the best of the strategy I had chosen and the result exceed all my expectations!

Naturally, I have players against which I’m more vulnerable, I think BrunoFelthes was the one I was struggling the most against, with a very good counter-dive strategy.

As you can see the code I wrote for this contest is far from being complex but was very efficient once all the details had been implemented.  I feel a bit sorry for players who spent a lot of time writing a complex simulator or implementing difficult strategies and ended with a lower rank but… yeah, that’s the game!


## Some feedback about the game
- I had fun writing strategies and trying to improve them without having to code a complex simulation -which I usually do- and spend most of the time debugging the engine and trying to fix my evaluation. That was also nice to have a contest very different from what we were used to.
- However, the diversity of strategies and the number of cases required to be handled is too high, which makes me feel that this kind of game doesn’t fit well for a 10 days contest. 
- Even if I don’t mind having complex rules, I can understand that it can discourages players. I think that the quality of the rules can be increased by adding pictures or just clarify them to help understand. I also think that the Wood 3 boss was too strong to be beaten by a first and simple strategy, which is something that can frustrate players.
- As many others said, a proper debug mode is mandatory for this kind of game.
- It was well balanced! Of course, some strategies are better than others, but globally the diversity of team compositions and strategies at top level shows that a lot of things were viable (I don’t know how the decision to nerf melees at a time when ranged were dominating the leaderboard was made, but it was very well anticipated!) 

I really want to congratulate AntiSquid, Illedan et Wildum for that great work they did on this game!

