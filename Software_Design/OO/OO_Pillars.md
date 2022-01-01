![Trees Cover Image](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/OO/imgs/cover_trees.png)

In every lecture or tutorial about we come across these keywords: Object, Class, Abstraction, Encapsulation, Inheritance, Polymorphism. This is the universe of the OO Programmer… Or is it ?

What is OO and why we use ?

Lets begin with the “Pillars”

## Encapsulation
_Bundling data with the functionality that operate on that data, or the restricting of direct access to some components._

Did we had encapsulation before the OO Languages ? Yes, in C we had perfect encapsulation. The header file contained the signatures of functions and data structures, on the other hand the a .c file would implement them.

The users of our functions and data structures would include  the header file never knowing anything about our implementation. Code exemple:

login.h
```C
void request_access(SecureKey key);
```
login.c
```C
void request_access(SecureKey x) {
	if (x == secret_key) {
		access_data_base_with_priveleges();
	} else {
		access_data_base();
	}
}
```

Object orientation weakened encapsulation. For exemple, C++ put all the variables in the header file, compromising its visibility. To control the access we had to introduce keywords: private, public, protected; so the compiler could tell what can be touched.
I want to exemplify with code this mechanism in a future post.

Encapsulation is present for sure but it's not the most attractive aspect of OO.


## Inheritance

_The mechanism of making new functionality and data structures from existing ones._

There was inheritance in C, although not very convenient.
A more detailed discussion is need here. I won't risk mentioning pointers and structs just yet and scare people. For now I say: "OO gave us slightly better inheritance".

We're going to prove it in future posts.
The way OO allows us to inherit behaviors and variables made programmers lives a little easier, although the decisive "Pillar" is the next.


## Polymorphism

_With a same signature for a mechanism it's possible to implement it in different forms._

In C, it's possible to do Polymorphism, it involves function signatures, pointers to functions and a table to store those pointers. In C++ this is how Virtual Tables are implemented, further discussion of this subject in another post.

OO Languages don't need pointers to functions because they have polymorphism. The C strategy was too dangerous, error prone.

C++ gave developers easy, cheap and safe polymorphism. And is Polymorphism the key of OO Programming.

We just saw the three famous concepts about OO we mentioned in the previous post. As we can see in our tree below it's almost time for the SOLID Principles.

![oo+solid](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/OO/imgs/oo%2Bsolid%2Bhierarchy.png)


## What OO Programming is all about

Let's think about a program, one bigger than Hello world!, it begins with a main file which call high level modules, those high level models call middle level modules and so forth util we reach the low level modules. It makes perfect sense, we begin our apps with general ideias in mind and the details come later.

High level calling lower levels is natural, but High Level Policy depending on Low Level Detail is problematic for software design. Imagine every time you change a little detail you have to recopile all your system: low level, mids and mids and middle levels then high level modules. Recompiling alone is enough of a problem imagine bugs on low level affecting your business rules in the most unexpected ways.

The Polymorphism is the main tool in OOP to solve this puzzle.
Our problem is in the red lines of the figure below(note that undesirable SCD can happen anywhere). We have to be careful with the Source Code Dependency[SCD] on low level detail, it can make the design Rigid, Fragile, Immobile and more - Design Smells can gives us more exemples on what can go bad.

![Dependency Structure](https://github.com/jptkao/Blog_posts/blob/main/Software_Design/OO/imgs/low_high_level_interactios.png)

Polymorphism provided us with absolute control of the dependency structure. So it's now possible to carefully choose what dependencies should be inverted to avoid the decay of software design.

The true power of OOP is now unveiled. Next we need to talk about the [Dependency Inversion Principle](), it's tightly coupled with this post's ideas.