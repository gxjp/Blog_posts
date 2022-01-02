![Cover DIP](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/SOLID/imgs/Dependency%20Inversion%20-%20Entry%20Image.png)

Oh hi! I hope you liked [The Object Orientation Pillars](https://dev.to/jptkao/object-orientation-pillars-22c7). We shall continue the discussion about dependencies and provide some exemples. This time we'll use UML diagrams to model our exemples. The exemples are a bit unconventional, remember the main object is to not forget about the ideas in here and use them to reason about your designs while coding.

## Dependencies

First we have to differentiate to kinds of dependencies:  

**Run Time Dependencies - RTD** occur when the running program access a module Butter through another module Bread, here Bread depends on Butter to continue the execution of the application. This change of location in the flow of control is very clear when we're using the debugger. We see our functions in one file calling functions from other files and when we 'step in' we go into another module, the module just before we *stepped in* depends on the module just entered. This dependencies occur whenever two modules interact at run time.

**Compile Time dependencies** when one identifier is defined in one module Beurre and is called on another module Pain, the calling module Pain has a Compile Time Dependency(or Source Code Dependency - SCD) on the defining module Beurre. It happens all the time, you call a function from another module and forget to import it: the compile won't succeed.  
The tree from the last post was drawn thinking about this kind of dependency. The tree was sad because High Level Policy depended on Low Level Detail.

![Sad Tree](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/OO/imgs/low_high_level_interactios.png)

Next we're going to see how to make happy Dependency Trees.

## Inverting Dependencies

We're going to use *Polymorphism* to force Run Time Dependency Structure and Source Code Dependency Structure to differ.

This is the first of a new series of marvelous exemples carefully thought for the SOLID Principles, I hope you like, or I would say: I hope you don't forget.

We're designing a game that simulates a universe we're superheroes exist. Our first design began with the class Bulk, he is a normal man that gets big, green, super strong and aggressive when a certain condition is matched.

*A priori* we wrote two classes: Bulk and Enrage. Bulk was responsible for the hero and Enrage for the transformation. We represent the code structure in the diagram below:

![Class diagram enrage bulk](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/SOLID/imgs/DIP%20Class%20Diagrams%20-%20UML%20-%201.png)

All worked well and stuff but we needed to separate responsibilities between teams: one would work on the Hero character and other on the Hero's behaviors. How could we rearrange our code so the work of the two teams would not colide ? 
There's no need to separate we all love to use Interactive Rebase before pushing to the repo...

Changed my mind again, better change the design.

In the new dependency structure the class Bulk use a Interface called Reactions. The interface declare the function *transform()*. The previous class Enrage now implements the interface. See Class diagram below:

![Class diagram with new interface](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/SOLID/imgs/DIP%20Class%20Diagrams%20-%20UML%20-%202.png)

Something changed, can you see how flexible it's now? Class Bulk does't know how is going to implement the _trasform()_ function, only at run time the implementation provided by Enrage class will respond to the message send by Bulk. This CTD is almost identical to the CTD of the first design. But the SCD is much different, Bulk's code need only Reactions interface to compile, and Enrage needs only to implement Reactions to compile. The Source Code Dependencies point against the flow of control. We inverted dependencies and made our code better for our necessities!

## Wow this is flexible!

One more exemple. Imagine the Behaviors team wants to add the means to transform our character, how would they do it ?

Very simple, create another class Fight which implements _transform_. At run time we would pass the new class to Bulk class and it would work perfectly. And the same could be done with more classes(I'm not saying you must do this with 20 different classes, think carefully [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)). One more diagram, note that the RTD will depend on whom is called at run time:

![Class diagram with multiple classes](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/SOLID/imgs/DIP%20Class%20Diagrams%20-%20UML%20-%203.png)


Next we gonna talk about spiders and the [Single Responsibility Principle]().