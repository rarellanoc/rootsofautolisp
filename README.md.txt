The roots of AutoLISP
Ricardo Arellano, 2023


'Programs must be written for people to read, and only incidentally for machines to execute.'
—Abelson & Sussman, Structure and Interpretation of Computer Programs. 


In 2002, Paul Graham, a very well-known programmer of the last decade, stated that the work of John McCarthy in 1960 is akin to what the Greek ancient Euclid did for geometry. 

That’s a bold statement. I only checked an Euclid book once, and it's a double-edged sword. The work is so careful that it seems dull, and given we learned (or were induced to learn these things in school) some things seem familiar. 

Recently visiting what the Renaissance Italian compilator, stage designer and architect Sebastiano Serlio took from Euclid, it seems that it hinges on arriving at simple definitions, specifically point, line, and plane. 

But even Serlio does not want to step into hard theorems, but rather ‘pick flowers from his most abundant gardens.’

Theorems are hard. But let’s pick one as an example. 

	⁃	If from equal parts we remove equal parts, the remaining parts will be equal. 

Then, in the work On Perspective, the notes from Serlio show that philosophical questions about what perspective is can be found in the book Optics. Which are tough things to deal with (even with cultural associations around). 

Enough with Euclid, for now. 

But. What I see in common is the ability to reduce common ground into a set of simple rules, or axioms to work with later. 

Maybe for some of you, computation might not be as interesting, but it might be as well cause of the abundant literature and procedures written in C style. 

This is different. Let’s start. 

Akin to defining what a point is, we can define an atom expression. 

It can be as simple as a sequence of letters like:

	⁃		foo

But the second type of expression is what is called a list, hereby the name of the language. 

	⁃		()
	⁃		(foo)
	⁃		(foo bar)

The caveat is, that a list can contain other lists. 

Like in:

	⁃		(a b (c) d)

It’s important to notice that, as in math, things can be solved or can return values. The implications of this are done for the aim of simplification. 

Math is not here to show exact relations in reality but to make us calculate and anticipate some behavior. At what angle do we need to throw a rock as far as we can? 

So, if we can say 1+1 returns 2.

We can also say:

	⁃		(quote a) 
	⁃		returns
	⁃		a

Quote is what is called a primitive as if it were an axiom. 

Atom is the next one we can define. It’s like a test. Returns t if is an atom or () if not. This is akin and used to represent truth. 

This, again, is a deep philosophical inquiry, like judging length. We need at least two objects to judge them by length. 

Another shortcut we will take is abbreviations. 

In this case;

	⁃		(quote a) as 'a

So,

	⁃		(atom ‘a)
	⁃		t

	⁃		(atom ‘(a b c))
	⁃		()

	⁃		(atom '())
	⁃		t

It is only by using the evaluator of truth that we can see what quote is for:

By quoting a list we protect it from evaluation. In the same way, we use quotes for saying town names, returning a description, or (if we quote it) revealing the number of words of that town name. This is the very distinction we will make between code and data. Kind of subtle at this point. Kind of the same. 

	⁃		(atom (atom ‘a))
	⁃		t

	⁃		(atom ‘(atom ‘a))
	⁃		()

If we continue, we will find other primitives. The operator is always first. 

If we call that kind of operators a function, we might need a new notation to describe functions. This builds up. 

A function in math is somewhat different, or rather a simplified version of its computational counterpart. 

In math functions, we exchange an x for taking place of a number. And any time we see the x, we replace it with 5, for example. 

In this notation, we exchange the same way. 

But the first element is now different and is somehow bigger. 

We will call that expression: lambda. (it’s a convention from the ’60s, from Alonso Church lambda calculus). 

	⁃		((lambda (x) (cons x ‘(b)) ‘a)

In this function, we replace any occurrence of x with the position in the third group, in this case, ‘a. 

	⁃		returns:
	⁃		(a b)

We can do it double, or we can make it outside our primitives. 

By the way, cons is a primitive that joins. It’s an essential feature of the language, but there is something else here. We’ll later see what a feature even is (because is essential).

We can start creating functions that contain functions inside. Not a problem. 

	⁃		((lambda (f) (f ‘(b c)))
	⁃	 	  ‘(lambda (x) (cons 'a x)))

Parameters like 'f' or 'x' can be used as operators or arguments (doesn’t matter that much). But this changes the game and gives us the ability to use a label. 

Let’s invent something called subst. 
Subst behaves like this. 

	⁃		(subst ‘m ‘b ‘(a b (a b c) d)

	⁃		returns:

	⁃		(a m (a m c) d)

But to denote that function beforehand we might expand the explanation a bit:

	⁃	The first element is an expression x, which in this case is ‘m. 

	⁃	The second is an atom y, which in this case is ‘b.

	⁃	The third element is a list. 

What returns (if we have faith or a complete system at hand) a list like the third element, but with new exchanges. 

Just like lambda, the label adds the property of replacing the first element after label, say f, and will find it in e to be replaced. 

It states that if z equals y, return x, otherwise keep searching. 

This presents us with a problem for the sake of simplicity, but we can already see where this is going. 

The surprise is we can write eval. 

Eval is a function, a little longer. 
I don’t know exactly how to cover it here now. But describes the entire mechanic of substitutions and labeling into one compendium, understandable by humans and at the same time, executable. 

The question that arose the first time I read this paper was:

	⁃	what the heck is knowledge then?

This question hit me hard at the time. So that’s why I want to translate this into a common lay architect language, or rather into architecture lingo. 

What are machines then? What are machines that play with geometry then? 

If we can make a calculator we can make those substitutions. 

Do we need to play with point, line, and plane? Where do we stop? 

We can, but not for the reasons we expect. 

The point is, that the whole language hinges on the possibility of creating subst, but subst can only be created with a thing called eval. What we gained with eval, is creating any function, including primitives like quote (one of the most elemental ones). 

One caveat. These functions are already defined in a way we don’t know internally, and we can’t be certain of the outcome of user-defined functions (the thing we did with subst for example). The good news is, that it is possible to redefine them (they are not blocked arbitrarily), thus giving control to the professional in charge. 

But let’s get back to math-deep questions. 

In school, we just assumed that by exchanging mentally x for 5 we can do x + 1 work for us (6 by the way) Now we have a computation for that. And not only that. 

…

Many questions can follow after this. 

I see some parallels. Waste in architecture as well as waste in computer flops. As Graham points out in the essay 'The hundred-year Language'. 

We can think that with computation we waste less time (making things and repetition less of a hassle) but here I think we will use time differently. Not just for doing things more efficiently (because, heck, the computer is sold for efficiency right?). But maybe using tediousness as a purpose. 

I have some prior experience with Processing, a language in the C style that artists used, until the advent of AI tools at least for the creation of computational art. 

Processing is a system created at MIT (Boston, again) simplified for artists to get visual output, and at least for me acted like a bridge between art and engineering. Generally with a shiny output. 

But the aim was different. 

Current formalizations (like the functions, or simple axioms) can act like a stronger scaffolding. 

Not in the throwaway sense, but as stable conceptual support. Ideally, because machinery always tends to disappear once is working perfectly. 

As of today, support for Autolisp has varied over the years, and compatibility is still an issue. We have to be careful to check the requirements and the capabilities of our machines (if they are really ours), otherwise, we will spend hours on setup, and not on loading or documenting our projects, which is the aim. 

For now, this might be the thing, a language used only to formalize decisions. The actual code that runs and the corresponding resulting image is just an afterthought. Execution is not necessary, not the aim. 

The final question is: What if we don’t really need to read and see the architectural plans, and we can just read the code to understand the building, and then run the code to see the plans only for the media, but not for builders. 

I don’t know if that is even possible. 

As I take ‘The code-writing Workbook’, a book by an Illinois professor, it seems that running the programs is the primary concern. Of course. Nowadays it is. 

Most plans are to be read visually by the builders. If there’s some need to build a terrace, why do I need formalization to build it? Or to hand out the design? The builder would not understand the actual programming code, for sure. 

But that’s maybe only training and propaganda. If he has the option to build with machinery (construction with mechanical pouring machines for instance) or to understand and build himself from the same language and expressions, that would be neat. 

Transformations like the ones presented in my GitHub.com (a shared library) repository 'operations' are not that interesting, nor are the random operations used. Which is disproved by the need to confirm them. The good thing is the availability of transformations. Operating on a higher ground than most designers. We know that. 

The search for forms is also part of the shared experience. As in the test of sound halls (Mendes) by testing shapes against simulated sound output. Or energy consumption (Troncoso & Garcia). 

Then, somewhere, will be time to see how the computer reads our instructions. We need to do this to check for errors. 

There are some things I learned when touching the computer for implementation. Let’s consider these as pointers. 

	⁃	Using and typing directly Autocad commands is not the same as defining them in an AutoLISP file we load later. 
	⁃	Writing again the primitives mentioned (functions) can break the system because the pre-installed functions will not be available.
	⁃	We have to be careful to Not ask for user input. The code should be the drawing. Standalone. (We don’t care about parametrical stuff, for now)
	⁃	If we follow the above rule, a few other commands and lines on the AutoLISP script should be defined, which reduces readability (Window screen viewport or redraw commands)

Then, we could ask what Alan Perlis, one of the fathers of modern computation asked: Towards what end?

Then we get back to the initial quote of Sussman: to be read. 

Running it becomes secondary, which means this whole enterprise will be for the aim of documenting, first and foremost, and then the readability of the code will still hinge only on education, in ways yet to be determined. 

…

AutoLISP is a dialect of the programming language Lisp built specifically for use with the full version of AutoCAD and its derivatives.
















































