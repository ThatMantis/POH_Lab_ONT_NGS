---
title: "Introduction to the Bash Shell"
teaching: 60
source: md
questions:
- "What is the bash shell?"
- "Why use the bash shell?"
- "How to use the bash shell?"
objectives:
- "Understand how the bash shell relates to the Operating System."
- "Explain when and why command line interfaces should be used."
- "Understand the basics of using the bash shell."
---

> ## Prerequisites
>
> From this point onwards, users should have a working Bash Shell setup!
> 
{: .prereq}

### About Bash

We are all familiar with the use of Graphical User Interfaces (GUIs) - for most of us, we encounter and use them almost everyday in our lives, whether we know it or not! The moment we login into Windows, and open up File Explorer, Internet Browsers etc. we are already using a GUI. The use of GUIs make our interaction with computers intuitive and user-friendly, and may be great for those preferring a more visual approach. However they may also be less efficient, and may offer us less control over our systems. Our possible options and settings become limited to the "buttons" available for us to click and press. In spme specific niche use cases, GUI programs might not be available at all, or at least in the way we need! 

This is where Command Line Interfaces (CLIs) come to the rescue. While CLIs may be less user-friendly and accessible; and possibly daunting to use for the uninitiated. They often offer greater control and efficiency. With CLIs, we are presented a whole combination of commands and parameters to choose from -- instead of just being limited to the buttons available with GUIs. With CLIs, we can now also run a variety of specialized tools and resources! This can be especially relevant in bioinformatics, where the bulk of tools and programs are usually Command Line Programs rather than GUIs. In fact, even many GUIs based programs are still Command Line Programs, with a "graphical wrapper" placed over them (e.g. EPI2ME and certain workflows in MinKNOW)! These GUI based programs often offer less space for customisation of parameters, with many options hidden from the user -- compared to if they were to actually run the actual program or workflow on the Command Line!

For instance, if we were to try running basecalling seperately (via Analysis>Basecalling) after a sequencing run on the MinKNOW UI...

![Basecalling on MinKNOW](../fig/basecalling_on_MinKNOW.png)

Compared to trying basecalling seperately using Guppy on the Command Line...

![Basecalling on Guppy via CMD](../fig/basecalling_on_guppy_cmd.png)

Notice how limited the run options on MinKNOW are compared to the options available on the command line! Most significant might be how there isn't even an option for read quality score filtering in MinKNOW here (defaults to qScore 10, which should be enough for most of us). The options presented on MinKNOW are just the essentials needed -- possibly to declutter the screen and make it easier to interact. Whereas on the command line there are so much more options available that one screen is not enough to list all the parameters -- and frankly could become a headache to read!

For this segment, note that the intention is to not make us experts at using the Bash Shell -- 1 Hour is probably not enough! Instead we will be going through the basics of the Bash Shell, and linking it as much as possible to GUIs, such as the Windows Explorer, so that it becomes less daunting for the beginner so that they can start using the other command line based data processing programs we will go thru for the later half of the workshop!

### Navigating Files and Directories



#<p> </p>
