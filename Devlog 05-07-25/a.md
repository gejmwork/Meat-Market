# Meat Market.

Since around November/December 2024 I've been working on Meat Market (I like to get ahead of new year's resolutions). It's been fun. It's also been completely and utterly awful. I suppose that's to be expected.

## What is it?
Well, it's a video game. Specifically, it's a video game about being a doctor. Not a nice doctor though. You steal genetic information from your patients, hunt down people with juicy organs to rip them out for profit, and forcefully implant them and your own macabre creations into your employees. What? They signed a contract. It's not like they can refuse.

What I'm trying to create is an environment where the player wants to feel powerful. Sure, they can beat up the weakest npcs from the start, but there will always be someone bigger. Someone stronger. I want the player to have to improve themselves and their ‘employees’ (read: indentured servitude). Challenge is OK. Tactical challenge is better. Hitting a wall on what they can accomplish with what they have should make the player adapt. 

The key here will be humanising their actions. Having difficulty beating this enemy? Easy fix. Go kill someone else and take their heart. They might be a mother or a father, but eventually, the player won't care. You won't care. See, the player character is also an employee, one with very heavy debts to a big old mega corporation. Don't want to kill them? Fine. Better find another way to pay off your debts and get stronger.

Note that this shouldn't be impossible. A truly good and altruistic playstyle shouldn't be discouraged outside of gameplay. It's a harder road because of the world. Shortcuts however will always hurt someone. It's up to the player to take them when and where they arise.

Anyway, enough about philosophy and game design. What have I actually done so far? Well, how about a random list.

## What's been done?

**Basic npc behaviour:** I grew up playing lots of God games - Black and White and Dungeon Keeper (R.I.P Lionhead Studios). They were always really fun to play, and what was more interesting to me was watching the NPCs wander about and do stuff. Not just standing there and running the same idle animation over and over again. It’s so much more immersive when they act semi-normally.

More recently, Shadows of Doubt and the Shadow of Mordor/War games have done something similar. Shadows of Doubt has its NPCs having a workplace, areas they frequent, and a home. I want to replicate that. Why? Because it’s cool and I like the idea of it. It’s a big job. But that’s what makes it worth it. 

Right now, things are very simple. NPCs go to set locations and wait for a trigger (the player interacts with them) before going to the next stage. I’m already quite pleased with it though. They have pathfinding and different states (combat/bystander/customer). What I want them to have is a bit of randomness. You don’t have the same exact route in your supermarket, you don’t buy the exact same things every time. That can come later though. My NPCs will be fully-fledged robots until the day there’s something out there for them that isn’t cold, empirical logic.

**Organ crafting:** This one has been a doozy. Initially, I thought about having the player shape and mold organs by hand, allowing them to form new, weird globules with different effects. Then i realized i was a fucking lunatic and simplified it drastically. (I’m not being facetious here; if I could’ve pulled that off I would’ve sold it to a medical company instead of making a game).

Instead, organs are made up of organ parts. Those organ parts define what benefit an organ has, and said benefits increase with adjacency. The plan is to make adjacency bonuses quite generous in what they apply to, as I don’t want to force anything standard. Why not have a liver-heart? Go on, you’ve earned it. 

For players who hate the idea of crafting stuff like that, I’m making lots and lots of prefabs. Why should I exclude potential players who hate the idea of slaving over a terminal trying to min-max their seventeenth new organ? Why should I force players to repeatedly make new organs for every use-case when they just want to relax after work? Answer: I shouldn’t.

Also, I randomly generate some organs.

**Random Generation:** Oh yes. Everyone loves random generation! Especially me, because I don’t have to do any actual work…

On a serious note, here’s the process:
I randomly generate organs and store them in a database.
I randomly generate NPCs and store them in a database.
I randomly generate their bodies - the organs they have.

Sadly, I haven’t gotten much further. You may be celebrating that fact. However, these NPCs will have areas that they frequent, activities they enjoy, and so on. I’ll need to retrieve them whenever the player is near those areas and turn some simulated nonsense into a nonsensical game object in the world. And that will be done with Object Pooling.

**Object Pooling:** Nobody in their right mind has thousands and thousands of game objects in a scene constantly active (unless you’re really mental or really good at optimisation). Generating these objects can take time, and you have to manage them on the back-end. 

Enter Object Pooling. You generate say, 1,000 inactive gameobjects and load data into them when needed. Afterwards, you deactivate them. Because of this, I have a hard limit on how many NPCs and such can ever be active at one time. This is a good thing. I would mess things up otherwise and have a bajillion guys called Greg trying to kill the player.


**Inventory system:** Pretty simple. Think Resident Evil. Items have dimensions. You pick up an item. You put it in your inventory.

**Shop management:** You’re not just a Doctor, you run a little shop too! You put things on shelves and people pay for them at the till!

**Currency:** There are currently two types of currency, with an additional one planned. They are:
- Credits: your standard cash money. This is what you buy most things with.
- Genecode: want to make organs? Want to genetically modify people? Who doesn’t? Want to research new fields of genetic/biological technology? Well, every study needs a test subject or two. You need Genecode. You can harvest it from (un)willing donors in droves, or you can skim little bits from your business operations. A used needle? Genecode. Wrapper from a burger? Genecode. The dirty credit bills that people throw at strip clubs? Way too much Genecode.

- Biomatter (unimplemented): like Genecode, this is mostly gathered from biological matter. But where Genecode are the little specks of gold dust, Biomatter is the dirty, muddy river where you find it. It’s not refined or useful enough for anything special, but it’s a great construction material. It’s the primary resource used for building, general crafting, and so on.  Right now it’s unimplemented. There isn’t much to build or make.

**Injury treatment:** Not everyone needs a new heart. Lots of people get boo-boos that need a plaster. Injuries have different treatments of varying effectiveness. Some treatments will make an injury worse. Some are vastly unprofitable. Better find the right one. It's intended to be a good source for Genecode early on and to maintain a high overhead of customers without overtaxing the player's time and resources in surgery.

**Surgery:** One of my initial concerns about Meat Market was that surgery would be too complicated. It would be ridiculous to assume that over 0.01% of players actually know how to perform surgery, and if I tried to make them learn it would end up catastrophic. Despite the premise, surgery isn’t a selling point. Customization is. Creating weird, messed-up monstrosities and watching them fight is the whole point. 

With that in mind, I’ve simplified surgery down to the bare minimum. It builds off the inventory system by having you place organs (inventory objects) into a body part (inventory), with the added twist of these organs changing the stats of the donor. Those stats are pretty barebones right now - there’s nothing for them to really do other than bump up a score - but I have big plans for that. I’m  also going to be adding adjacency bonuses for certain organs/organ parts. As before however, it just bumps up stats. Nothing exciting.

**The usual suspects:** movement, combat, etc. It's standard stuff right now, but I plan on changing it. As of now, all I can say is that it exists and works.

**Dialogue:** I'm not sure if I've approached this correctly. The current architecture has dialogue choices (which contain npc text, the players text, and some utility stuff like if it links to a quest) housed in dialogue trees. Dialogue choices lead to dialogue trees. This is good because it means I can make new dialogue paths just by linking different dialogue choices to different dialogue trees. It adds variety. Spice, even. 

However, it's bad because it's a pain in the arse to manage. Gameplay wise there isn't a difference, so it's all about which method is easier for me. That's a nice change, isn't it? Realistically I'm probably not going to end up changing it. I don't have the introspection or foresight to know which method will be better in the future. By the time I do, I'll have settled into the current method.

And that’s about it as to what I have currently. 

## What comes next?

So what’s the next step? Don’t know. I’ll let you know when it’s in the game.

However, I want to talk a little about the setting. Unlike the mechanics and the code and the art, it’s something that hasn’t changed much since I started making it. See, I adore moral quandaries. They make choices interesting, and they make worlds engaging. I can’t tell you the number of times I’ve played a game and not given a shit about which decision to make, so when a hard choice is in front of me, I remember it.

Meat Market is in a world of hard choices. By your very nature as the player character, you embody a predator and a healer. I want you to imagine something for a moment (ooh, literary writing).

Walls of living concrete hum as you stroll past. Bioluminescent greens and blues flicker on the pavement before you, and all around are a menagerie of creatures. Tentacles. Claws. Buckled legs and twisted spines. They are your creations. They were moulded by you, shaped for specific purposes. Yet when you look at them you can still see something. A light in the eyes, or whatever remains of that behind them. And you know that they were once human.

Are you guilty of this? Or do you blame those who have a boot on your neck? Or do you not care? Do you enjoy it? 

What do you do, in those shifting streets, when amongst your horde of monsters and men, your tools, the heady scent of rich genecode wriggles into your nostrils? Are they to be an ally, a possible employee? Or are they simply prey? You have debts to pay, after all.

Meat Market is Biopunk. The setting will embody those central aspects of bio-enhancement, megacorporations, and an authoritarian, unjust society entirely. It will be up to the player to reject those principles and play a harder game because of it, or to embrace them. This is the intended route I will take when building the setting. I mentioned NPCs earlier - they have to be humanised. That will probably be one of the hardest parts of development, but it is critical.


If you made it this far, Jesus Christ, sorry. If you just skipped it all and went to the bottom, wise choice. Also, if you expected handy pictures or videos, sorry. This wall of text wasn’t for your benefit. It was for me.
