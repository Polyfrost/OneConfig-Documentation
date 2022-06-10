---
description: Learn about how Minecraft Modding works, Java, and how to make Minecraft mods
---

# Getting Started with Modding

## Getting Started: What is modding?

Welcome to Minecraft modding! These next few pages will serve as a basic guide for how to get started with Minecraft modding, how to use IntelliJ, Gradle and some Java basics. Minecraft mods are added to the game most commonly using a **loader**, such as [Fabric](https://fabricmc.net) or [Forge](https://files.minecraftforge.net/). The term 'mod' refers to modification for a game, Minecraft in our case. Minecraft is written in Java, so naturally so are its mods.

**You will need some basic knowledge of coding to do this.** But don't worry! Java is reasonably easy to pick up, being an Object Orientated Programming (OoP) language with a reasonably easy to understand syntax. You might want to watch a YouTube tutorial on Java before you begin to help you out.

## Step 1: Installing IntelliJ IDEA

For this tutorial, we are going to use the OneConfig Example Mod [**which can be found here**](https://github.com/Polyfrost/OneConfigExampleMod)**.** We are going to use IntelliJ IDEA as our IDE for our coding, and this is the IDE of choice for many mod developers and Java developers.

Firstly, head to [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/) and download the IDE for your platform, in my case Windows. I recommend the Community Edition for casual developers as it has all the features you need - and its free! Download, and follow the prompts to get it installed.

Once that has downloaded, Open up your File Explorer, and create yourself a directory for all your mods, for example **C:/Users/Bob/Documents/Minecraft Mods/.**

## Step 2: Creating the Project

Great job! You have installed IntelliJ and are ready to clone the project. Now, open up IntelliJ and you should be greeted with a screen a bit like this (make sure to accept the terms first):

![IntelliJ Welcome screen](<../.gitbook/assets/image (3) (1).png>)

Now, click **Get from VCS** and go to **Repository URL** and check that **Version Control** is set to **Git**. Next, **set the directory to that root folder you made earlier**, and in the **URL** box input [https://github.com/Polyfrost/OneConfigExampleMod](https://github.com/Polyfrost/OneConfigExampleMod). Add the **name of your mod to the end of the end of the directory**, so for this tutorial I'm just going to call it "ExampleMod". It should now look something like this:

![IntelliJ Clone screen](<../.gitbook/assets/image (5) (1).png>)

If that all looks good, go ahead and click **Clone** and click Next below to continue with the guide!
