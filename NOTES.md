== Test Driven Development

Of course, we walk the walk: we practice continuous integration (CI) and continuous delivery (CD). We do test-drive development. We use cloud computing. All these things translate into better results, faster, and so its hard to write a chapter like this one, focused on testing, seemingly to the exclusino of all these other wonderful practices. We're going to focus on testing, and we're even going to try to do test-driven development (TDD).

TDD is, simply, the act of writing tests first. Before you've written a line of production code, you write tests that test the production code. Which is hard to do if you've not written the production code. Because there are no types against which to compile. So you end up having to write the minimum to get the compiler happy, then going back to flesh out the test. But you don't want to write too much of the test. You're just trying to prove out one thing in the production code, after all. So, you end up in this tight loop that might seem at first very frustrating. Bob Martin describes the the three rules of TDD as follows:

* You are not allowed to write any production code unless it is to make a failing unit test pass.
* You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.
* You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

With a statically typed language like Java you end up in a continuous loop writing tests, then writing the code to make the test compile and then pass and then going back to test code and so on. At first this seems.. constraining. You'll like it once you get the hang of it. TDD has some profound benefits. A team doing TDD is at most a few cmd / ctrl + Z's away from green, production-worthy code. A team doing TDD gets the tests done at the same time as the feature is implemented. The endorphin hit of successfuly implementing a feature arrives at the same time members of the team otherwise get the code tested. It no longer feels like a _chore_, like documentation, which must be cared for, but feels like a lesser priority. The agile manifesto says "value working code _over_ comprehensive documentation." With TDD, you have working code _and_ proof that the code works at the same time. If you use something like JavaDocs and TDD, then you can get pretty good documentation at the same time as you deliver the working tests, too! For more on Spring REST Docs, you might check out O'Reilly's _Cloud Native Java_.

So, clearly, I'm a big fan of TDD, but it can be hard to demonstrate its execution in a book! So, here's what I'm going to do. We'll introduce the test code first, as the need arises, and then look at the production code that satisfies the tests. I (mostly) won't introduce fragements of tests. It's _really_ tedious to do TDD in a book!

== Inside-Out or Outside-In

It depends I suppose on the team and their style, and the style of the individual, but you have to decide upon whether you want to write tests for the inner-most components first and then work your way out to the API-layer and UI, testing as you go, or if you want to do things in reverse, starting with the UI and then working your way inwards. The inside-out approach has sometimes been called "Chicago-style."

Here are, as best as I can understand, the differences in approach. Imagine you're building a complex system. In an inside-out approach you'd start with the individuwal entities and start fleshing out their behaviors at higher layers. Eventually, at higher layers, you'd start assembling individual pieces. Now, some might say that this asssembly, this _integration_, is where the risk is and that definition should be cared for first, before you get into the small and perhaps even meaningless entities that support the integration. I'd argue that its easier to parallelize work if you start from the inside-out; people can pick a part of the application they'd like to work on and work streams converge at the integration tier.

I like to go inside-out: I'll start fleshing out the business entity and work my way towards the interface. If you're just building an API (an HTTP API or an RPC API), then that API is the "interface." In this way I'm deferring potentially risky integrations until a little later and  hopefully  - in a microservices world - that integration is still rather small and controlled by folks on the same team. That is, "integration" isn't as scary if it's all being done by the same person or set of folks on a small enough team.

Microservices are all about acheiving autonomy and reducing the cost of coordination, but that doesn't mean you eliminate coordination! Just reduce it. Your mileage may vary and I'm here to tell you that I don't have a very strong opinion about it one way or another; I just want to provide background about how I'm going to approach this chapter: inside-out.