---
title: "Choice: The Art of Doing Things Well"
categories:
  - Programming Languages
tags:
  - Choice
hidden: true
---


There is a big difference between trying to do something and trying to do something well. They represent different modalities of action and no good comes from conflating them.

By "trying to do something well", I mean almost any way to compare different products. In a process, it could be performance, memory usage, or binary size. In a service, it could be latency, throughput, network usage, scalability, robustness, or cost. It could be things like accuracy, precision, efficiency, effectiveness, user experience, and appearance. Essentially, it is any time you prefer one variation over another when both are correct.

That is not to say that simply doing something is easy. In fact, it is also quite difficult. It is sometimes called essential complexity, but correctness complexity might be a better term. If you have programmed without worrying about performance, you would know that essential complexity is still hard to manage.

Even with this, I don't know of any field besides software development that has such high requirements on both correctness complexity and doing things well. The correctness complexity comes from the difficult concepts to learn and manage. They might come from math like computer theorem proving. They might be any field using computers like science, medicine, simulations, or large complex systems. Finally, any large code base or business logic becomes it's own complex field.

Likewise, the engineering requirements are also high. That doesn't mean every project demands it, but there are a great many that do need the highest standards of engineering excellence. This includes fields like compilers, super computers, high performance computing, and large-scale highly-available web services.

To better understand this difference between correctness and doing things well, I want to mention a few important properties. First, the existence of a way to do something well implies there also exists a way to do something poorly. That means two ways to do things. In reality, there is often many more than two. When you consider combining multiple different choices like algorithms, data types, and data structures made in tandem, then the total options explodes exponentially.

The second property is that there is rarely a perfect option. You can't just say you'll choose the good way to do something instead of the bad. Which one is the best option is often nuanced and situational. There are tradeoffs between the options.

As an example, imagine we want to create a list. There are many kinds of lists. We could have a good old-fashioned array for fixed size data with fast indexing. There is also an appendable arrayList or a deque that can handle prepending too. There are linked lists for inserting into the middle of a list. There is a chunk list, a tree list for immutability, or a hash list for sparse data. You might use a function from index to value as a list. Or, use a stateful generator or iterator that produces list elements as it goes.

So, there are a lot of options. Picking the right one requires a good understanding of the context. You need to know what kind of data it contains, what the source of the data is, and what kinds of operations you might be doing on the list. Each option has strengths and weaknesses, and none is the best in every situation.

This is the same kind of pattern you will usually see. Rarely does there exist a perfect implementation of a data type, or a data structure, or an algorithm, or an architecture, or a style, or a color. There are always these kinds of options and tradeoffs and nuances and special cases. Only by understanding the context can you make the right choices to do it well.

The final principle I want to reiterate is how to manage correctness complexity. The basic principle is decomposition. We take the unmanageable whole complexity and try to break it up into more manageable chunks. This is especially true when chunks are reusable or they reflect pieces which are orthogonal.

But, our goal isn't simply to break it up into chunks. We want the chunks to be as divorced as possible. Otherwise, you aren't much better off than having the merged chunks. As programmers, we have a lot of terms about this.

Take abstraction. The idea is that you can divide a chunk into an interface and an implementation. Then, you can use it by understanding only the interface, but without having to learn the implementation. This is even more powerful when many implementation chunks can share the same interface. Then, you only need to learn one interface chunk and can use many implementation chunks.

There is also the single layer of abstraction principle. It says that when one chunk interacts with another chunk, you should use ideas coming from only those two chunks. This helps reduce the number of chunks you have to understand to work with a piece of code.

You will also find similar ideas under separation of concerns or "domains" and "subdomains" in domain driven development. Here is the general principle. When decomposing your larger body of knowledge into chunks, minimize the connections between the chunks. Only necessary information, knowledge, and context should flow between the chunks.

But, we have reached a contradiction. To do things well, it is necessary to both have and use context. To manage conceptual complexity it is necessary to remove and ignore context. And, this tradeoff should match your intuition as well.

One example is integer data types. In Python, they always use a BigInt. This is quite inefficient. The best thing to do is to use the smallest int type (int8, int16, int32, etc.) that fits the data. But, Python is unable to automatically determine how big an integer might be. So, it has a few bad choices. It can expose this piece of implicit complexity and force users to make a manual choice. It can choose something that sometimes doesn't work. Or, it can always choose the slowest and most robust option of BitInt. It chooses the BigInt. The same applies to much of high-level vs low-level situations.

You may have experienced this with APIs that expose configuration options for performance. Although they can boost performance, it comes at the cost of making your code more complicated. Once you start worrying about performance, your code jumps from simpler to drowning in incidental complexity at shocking speed.

Fortunately, the problem is resolvable. The key realization is that choice is supplemental. So, rather than trying to mix it into existing code, it needs to instead amend it.

Before moving on, let me summarize this notion. Hopefully, it will also help crystallize it into an easy to apply form. The basic premise is that every action (function) has three steps:

1. **What** - What do you want to do? As our example, let's continue with creating a list.
2. **Options** - What are the options you can take? Here, it would be the fixed size array, LinkedList, HashList, etc.
3. **Choice** - Which choice should you make and when should you make it?

Note that while this pattern is being applied to code, it is a fundamental problem with making decisions. Imagine that we humans are trying to make a decision. We may write up a small document or presentation explaining it. It would have an introduction explaining **what** the problem is. Then, it would list the **options**, probably with some pros and cons to help explain why we are making the choice. Finally, it would end with the actual **choice** as a conclusion.

Now, the pros vs cons case is a bit simpler because it involves only one situation. If we were trying to explain many situations, our tool might instead be a decision tree or flow chart. In this case, the internal nodes of the flow chart describe when to make the choice and the leaf nodes describe what choice to make. It's the same pattern.

That's because choice is a fundamental problem. It is the type of problem which is wide-spread and affects lots of different domains. Many people will face it, and recognize it, or at least recognize part of it. For the fragment they recognize, they often give it different names and terminology.

Let me name a few of these synonyms of choice now. One of the first one is design, such as the design of system architectures or the design of websites. Under this terminology, the **what** is equal to design requirements, **options** as the design choices or design space, and **choice** is the actual process of design.

Or, take optimization. It is a subset of the problem of choice of when there is a numerical way to evaluate a set of choices. Next, you have to specify a set of choices that you want to optimize. Given this, you can search through the space of choices to find the top scoring one.

Another is many instances of configuration. For example, think about a function that accepts some configuration. The function becomes the **what** and the configuration allows you to control choices when executing it. But, this is a very manual implementation of choice.

A final example is experience. Or, you might call it some kinds of cognitive tacit knowledge. It has the main trait that is can't be easily explained.

As programmers, this should be especially easy to understand. If we were to explain how to do something, we would use a function. This means that the explanation is bounded because it fits between the begin curly brace and end curly brace. Or an indented block, but that's a bit less dramatic. Even if you consider "prerequisite knowledge" (other types and functions used within the definition), you can recurse through them all and then it is still a fixed set of concepts.

But, choice is not fixed. It is situational and there is no way to produce the best possible choice in every possible situation. That is even assuming a best possible choice exists. Many have a tradeoff of two factors like latency vs cost. Then it depends on what you value more in the situation.

Even if there was a best choice, any strategy you can learn ends up being a heuristic to find good choices in some subset of the problem. The only thing to do is learn more heuristics, more comprehensive heuristics, and more accurate heuristics. Everything beyond that you have to figure out yourself on a case-by-case basis.

Actually, the problem is even harder because the options aren't fixed either. Let's say you do manage to develop the perfect heuristic to determine the right choice of list for every possible situation. But, what if tomorrow someone develops a new kind of list. Maybe it is a hyper-specific domain specialized list. Now, you have to reevaluate all those situations all over again to take this new kind of list into account. The same guidance applies that you have to keep learning and thinking.

Now, I have spent all this time merely introducing the problem of choice. What would an actual implementation of it look like? There are a few which implements choice as frameworks. But, this has two problems. One is that it is too pervasive and affects almost every bit of code. Second is that the compiler should often make the choice during build time rather than run time.

So, it belongs as part of the programming language. Right now, the only language that acknowledges it is [Catln](catln.dev/). It is also the language that I am developing.

To implement it, the plan is just the earlier definition of **what**, **options**, and **choice**. It only requires two language features. The first feature is the **what** and **options**, an interface function.

An interface function is a function that can have multiple definitions. The signature of the interface function then corresponds to the **what** and the definitions correspond to the **options**. All code should then try to use these interface functions rather than the implementations of them.

There are a few ways to think about calling interface functions. The first is that it follows the maxim "program to the interface, not the implementation". This makes your code more generic, reusable for different implementations, and more powerful for it.

Also quite useful is that this should correspond to high readability. It helps reduce out as many details as possible so that the code can focus on the simplest high-level description of the problem.

Another way to think about this use of interface functions is like C++ templates. If you think about functions as low level, they have a 1:1 correspondence to binary produced. But, there is no reason the compiler can't produce different binaries with different choices for different usages. It will cost binary size, but often that tradeoff can be worth it.

You can also think about it as maximizing choices. The more and more powerful interface functions that you use, the more choices you have available to you later. It may even produce choices that you wouldn't have thought of otherwise.

The final way I will suggest it to think about it like postponing a choice. Let's say you are reading through some code and come across a usage of an `ArrayList`. Now, did the programmer choose an `ArrayList` after lots of careful thought and experimentation. Or, did they assume it seemed reasonable enough and they had to choose something.

The problem is that languages without interface functions force you to always make choices. With interface functions, you can leave these thoughtless choices for later or someone else. It also means that you know where deliberation occurred and where it didn't. And, it highlights where deliberation should include comments explaining it.

So far, you have declared an interface function and used it in the code. The next missing functionality is to provide implementations of the interface function. These work like most implementations of an interface, interface function, or type class. The only minor thing to keep in mind is that there needs to be a name attached to each implementation so you can refer to them later when making the choice.

The final part is the actual **choice**. Here, there is a bit more room for innovation for how to support it. Think about the example implementation I gave earlier: decision trees. While this version is easy to understand, it suffers from a lack of extensibility. Imagine you are importing a decision tree from a library (or several libraries!). It is not clear how to best override it. This includes extending it to new kinds of leaf nodes, modifying existing leaf nodes, or substituting internal branches.

Another model which is more accurate is from HTML+CSS. They are one of the few solutions that approach choice properly, although in a quite limited fashion. Specifically, it applies choice only to a function which you might describe as `render(HTML html)`. Here, the HTML describes the **what**. The HTML and CSS specifications define the **options** and the browsers implement them.

Then, the CSS describes the **choice**s. Consider the format of CSS. In consists of selectors and properties. The selectors describe a situation and the properties are the choices to apply in that situation. When two selectors both apply, the one which more precisely describes the situation takes precedence.

A similar structure would work for general choice beyond `render`. It extends well to new situations because they are just new choice rules. It only means a new semantic structure for choice is necessary in the language.

The downside is that this solution is greedy. It makes choices on a first-come-first-serve basis without any way to backtrack. This works fine for creative design where choices don't interact much. It doesn't work as well when they do interact such as memory management, data types, or most performance related choices.

Given this, my current plan is to have choice scores. Instead of a fixed choice at every opportunity, instead there is a score given. For a more clearer formulation, the score should be the probability that a particular choice is the right choice in the situation. The score for a whole path of choices is the product of their scores (probability that the path is the best choice). Then, finding the best set of choices is the shortest path problem and you can solve it with Dijkstra's algorithm.

While this is the best strategy I have thought of so far, there may be a better one. It may not be as good in cases that require large amounts of backtracking. If it takes a while to recognize that a choice is bad, it will still have to explore all the permutations of the bad choice. Still, we could improve the efficiency with a heuristic like A* or improve the speed with a semi-greedy approximation using beam search.

Now, there is also another important piece of choice which I haven't given enough emphasis to. Let's go back to our list example and decide that we want to create an ArrayList. But, there is another option when creating it: the initial capacity of the list.

If we give it too large of an initial capacity, it wastes the memory taken up by the unused capacity. If we give it too small an initial capacity and overflow it, then we have to copy it over to a larger list. So, we can save some performance by trying to be more accurate with the initial capacity.

In that sense, choosing an ArrayList is not a single option. It is an option for all possible initial capacities of the ArrayList.

In summary, there are two kinds of choices. First, there is a function choice which chooses between different function implementations. Second, there is argument choice where we pass in "optional" arguments using choice.

Often times, things which should be choice arguments are instead arguments with default values. At first glance, they both look pretty similar. But, there is an easy way to tell them apart. If you always know the value from the calling function, it is an optional argument. If you might want to pass the choice up the call stack, it is a choice function.

The final thing I want to mention about choice is with regard to metaprogramming. I define metaprogramming broadly as any process that accepts code as input, often producing other code. For example, it includes such tasks as compiling (producing assembly from source code) and building cloud services (producing scalable infrastructures from single-machine prototypes).

Metaprogramming code often contains many different choices it can take. A compiler could choose different data types, memory management schemes, strict/lazy, to parallelize or keep single threaded, etc. Building cloud services can choose different serving solutions like clusters or serverless, different databases, whether to integrate a component (more monolithic) or split it off (more micro-service), single-machine vs distributed, etc.

Most of these metaprogramming tools can come across as rigid and with poor performance. This makes sense, because it is difficult for them to effectively understand the context from their source code. The formulaic heuristics they use can only learn and apply so much context.

Choice has a lot of potential here in two ways. One is that it makes implementing such metaprogrmaming much easier. Knowing what options are possible and when to take what options are very different problems. Having a clear separation between these two problems will make it easier to create different options and systematically navigate the options once created.

On the usage side, it defines a clear mechanism to control the metaprogramming. You can define both singular actions and whole patterns to improve. For example, you might change the memory management scheme of every graph. Or, you could easily rearchitect your cloud system. Either way, it will give you far greater control because choices are easy to implement. And, it is so easy because the metaprogramming is doing all the heavy lifting for you.

If you have made it this far, hopefully you have some understanding of choice. Once you see it, you will start noticing how pervasive it is. Many different problems are equivalent to choice. Many difficulties come because there is no tool for choice. And hopefully, now that you understand it better then you can solve it better as well.
