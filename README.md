# Famicom Wars - First Strike

<p align="center">
  <img src="images/title.PNG" alt="Title"/>
</p>

This repo contains the patch for the NES game Famicom Wars, which implements "First Strike". This means that attacking units deal damage to defenders first, as opposed to simultaneous damage. This significantly helps alleviate the game from turning into a tedious slog.

## **Installation**  <a id="installation"></a>
To install the patch, follow these steps:
* Have a copy of the Famicom Wars .NES file (*These steps will override the existing file, so make sure to copy the original if you wish to have a vanilla version of the ROM*)
* Download the patch `Famicom_Wars-First_Strike.ips` from this repository
* Download [Lunar IPS](https://www.romhacking.net/utilities/240/), a program which can be used to apply the patch
* Run Lunar IPS
    * Select "Apply IPS Patch"
    * Locate the Famicom_Wars-First_Strike.ips file
    * Next, Locate the vanilla Famicom Wars .NES file (again, I suggest making a copy beforehand)
* Load the newly-patched ROM (.NES file) into your emulator of choice.

Note: This patch is (to my knowledge) compatible with existing translation patches. I highly recommend the [English patch](https://www.romhacking.net/translations/6828/) by Stardust Crusaders (et. al.), which I used while creating this patch.

# The Problem
Famicom Wars has a healthy legacy that spans even to this day, notably for being the fist entry in the *Wars* series. This eventually begat Advance Wars, one of my favorite games - but what's remarkable is just how similar the two games are to one-another. Or rather, how two games can be so similar to one another, but play completely differently. Advance Wars is *snappy* - units hit harder, there's CO powers to turn the tides, and playing against the CPU is *at least* an order of magnitude faster. Indeed, Advance Wars has the benefit of being made in the future, both on better hardware after a handful of sequels, this is certainly no fault to Famicom Wars. However, if I had to pick *one thing* that totally turns me off from playing Famicom Wars, it would be that most games turn into a total quagmire. 

Restated, Famicom Wars lacks *momentum*. Without momentum, units tend to pile up in the middle of the map, unable to make a real dent in one side or the other. The root of the issue, from my perspective, is that damage is done simultaneously. When you attack, you are punished; an infantry attacking another infantry means that both sides will roughly take 45% damage, minus their terrain bonuses. A full-HP infantry on a city will require between 3 and 4 attacking infantry to destroy it, each in turn receive chip damage (even the one which destroys it!). So you invest heavily in artillery, which only further punishes actions on either sides as breaking down "unit walls" is even harder here. 

So, with all thing combined: Simultaneous damage, stally and grindy matches, sluggish UI, even slower CPU decision making (albeit impressive for the era) - the game virtually unplayable. Even the most basic matches end up taking *hours*! Why would you ever play this over Advance Wars?

# The Solution
There are some things which are really, really hard to fix, perhaps bordering on technically impossible. Making the CPU player better or improving the UI to be a bit quicker on 1980s hardware is a fool's errand with little payoff. *But*, making one little change can have drastic consequences on the gameplay: First Strike.

The concept is fairly simple: unlike simultaneous damage, First Strike means that the attacker deals damage first, *then* the defender. This means that the damage done by the defender is less (as, their damage is proportional to their HP). 

<center>

| <p style="text-align: center;">Original</p> | <p style="text-align: center;">First Strike</p> |
|---|---|
| <img src="images/original_tank_v_tank.gif" style="width:342px" alt="fair game spider movement"/><br/>|<img src="images/first-strike_tank_v_tank.gif" style="width:342px" alt="base game spider movement"/> |
| <p style="text-align: center;"> Attacker (Red) gains no advantage. </p> | <p style="text-align: center;"> Attacker (Red) gains an advantage. </p>|

The results speak for themselves.

</center>

Now, there is an advantage to attacking your opponent. Now, there are consequences for careless troops deployment. Now there is urgency - now there is *momentum*.

# Technical Details
When I do these patches, the technical work swings somewhere between "Writing lots of 6502" or "Reading lots of 6502"; in this case it was the latter. This was an investigation; my notes go on and on, walking through several different sections of the code, trying to figure out wtf is going on. In the end, the actual patch is largely moving or copying existing code, and adding only a tiny bit (I think I "added" like 6 Opt Codes, totaling roughly 10 Byte pairs). I was able to do this because I had a good understanding of what was happening, and what I wanted to change.

## The goal
Instead of "simultaneous" damage, I wanted:

- The attacker attacks first, and the defender gets damaged
- After the defender is damaged:
    - If they're dead, do nothing
    - Else, deal damage to the attacker proportional to the defender's health

## Investigation
As stated, most of the work was very much orientation. This section details that.

### Where to begin

### My Units, Your Units

### The Great Big Damage Calcuation

### The Mystery Functions

### 

# Conclusion
I've made patches in the past to improve old games (see: [1](https://github.com/schil227/FantasticAdventuresOfDizzyFair), [2](https://github.com/schil227/JourneyToSiliusFair)), but I am especially pleased with this one. While those patches were focused on tweaking the difficulty to make the game more fun, this one's focus is to make it less boring. That said, it doesn't make the game *perfect*. There are some dubious unit match-ups: for example, a bomber does a pathetic 50% damage to infantry, while infantry (dudes literally standing on the f****** ground) do 5% damage. Apples to apples, the bomber has done 500G damage to the infantry, and the infantry has done 1000G damage to the bomber. That's ridiculous... but at least with this patch, the trade-off is an even 500G (still ridiculous). 

There is a [thriving community](https://awbw.amarriner.com/) which, in recent years, has seen a dramatic increase in players interested in Advance Wars. In that vein, I think there's still interest in Famicom Wars. This patch improves it, and makes it a lot more palatable to "modern" players - however, I think that a few more tweaks would really make this game shine. That said, I'll keep this change as a stand-alone patch, because a part of me really enjoys the "weirdness" of Famicom Wars, and I think those who dig into the past would enjoy it as well.

In the future, I may make a follow up patch to this; but until then, enjoy.