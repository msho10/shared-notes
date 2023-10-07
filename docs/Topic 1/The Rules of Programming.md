
#### Rule 1 - As simple as possible, but no simpler
See also [[Simplicity]]

Complexity is the ultimate enemy.
Code should be simple to read and to write, more than anything else.
If you can't simplify the solution, try simplify the problem.
A good solution should be simple yet enough to meet all the requirements of the problem.
#### Rule 2 - Bugs are contagious

The sooner you fix a bug, the less entanglements and dependencies you need to fix. The later is what makes bug fixing so time consuming and difficult.

Stateless functions are easier to test.
Codes that are easy to test tends to be easy to write too. That's the advantage of TDD. But there are situations that TDD doesn't work well. For example, when there are huge or endless combinations of inputs, or outputs that are hard to measure or quantify. Test what you can test and control what you can control.

Use internal testing (or audit) for to test state. This is better than exposing internal functions or properties just for the sake of testing. In addition to automated testing, code can continuously to test itself with internal testing.

Don't assume the caller (consumer, user) would know the details or the proper way of doing things. They are likely to make mistakes, but you are in a better position to catch them. It would be even better if you can avoid them in the first place.

To catch errors, it doesn't matter if you use asserts, exceptions or returning an error code. The important thing is to flag the error, not how you do the flagging.
#### Rule 3 - A good name is the best documentation

Minimizing mixing of different naming and conventions. This is hard to completely avoid. Maybe a wrapper can help, if a 3rd party library that has a different convention is used frequently and in many places.
#### Rule 4 - ==Generalization takes 3 examples==

If you got 1 use case, just write code to solve that case, DON'T try to guess the second case. Write code to solve problem that you understand, not the ones you are guessing at!

It's always easier to solve a problem with a solution that targets only the problem. Don't try to come up with a general solution that will solve more cases. This is because the assumptions or predictions you made are going to be wrong! You don't just waste time and effort in writing the code, but also in testing and maintaining it.

Generalize only if :
- there are 3 or more use cases
- the general solution makes the code easier to read and write. 
- the general solution should base *solely* on use cases that you already have in hand.

Premature generalization is actually worse than YAGNI. It creates the following problem:
- The general solution is almost always more complicated than a specific one, and this makes the coder harder to understand, to work with and to change. 
- Because of its complexity, it creates more bugs.
- Because of its complexity, it makes adapting to unanticipated use cases difficult.
- The general solution is sticky and you will be less likely to consider alternative solutions.
- The general solution will become more and more cumbersome over time. Once you have a template, you are likely to extend the template's functionality when new use cases appear, instead of reevaluating it. Gradually, you will lose sight of the context and are further and further away from the most simple, easy and straight forward solution. 
#### Rule 5 - The first lesson of optimization is don't optimize

Write simple and clear code first. It will be easy to make simple code to run fast. Complicated code have a higher chance of being slow.

Very serious or expensive performance issues do happen from the beginning (in the design). That's why it's important to do the math before writing any new code.

For code that have never been optimized, It's likely that you can get 5x to 10x speed gain with little effort.
==The way to make code faster is to DO LESS, instead of doing the same things faster!

5 steps for optimization:
1. Profile or measure your code
2. Make sure it's not a bug
3. Know your data
4. Plan and prototype
5. Optimize and repeat from step 1

Once you meet your performance target, don't do any more optimization. If you have more ideas, put them in comments and move on.
#### Rule 6 - Code reviews are good for 3 reasons

Code reviews are good for:
- finding bugs (by yourself or by your reviewer)
- share knowledge and gain a better understanding of the code.
- Motivate to write better code.

How it works:
- Reviewee prepares her code for review (look at the diff, clean up, make sure she can explain her code and why the changes). Usually reviewee would find some bugs at this time.
- Reviewer walks through the changes in diff. Reviewee provides comments and reviewer asks questions until they both understand the changes. Note reviewee should not drive the conversation. 
- Reviewer provides suggestions, tests cases, and discuss alternative approaches. Reviewee is responsible to note all the feedbacks and incorporate them.
- After changes are made, reviewee can submit the changes. If there are a lot of changes or they are big, it may need a re-review. Or if there are uncertainties or conflicts, another reviewer may be included.

The review process can take hours. Since you have spent so much time in the review process, you want it to be productive. You will think through what you want to get out of it and why. And get rid of things that are not helping and double down on those that help. As a result, you will be getting more out of it or spending less time. [[Effectiveness]][[Efficiency]]
#### Rule 7 - Eliminate failure cases

If you are writing error-handling code to account for errors in calling the function, that's a sign that something is seriously wrong. You should be designing an interface that makes incorrect usage impossible. Detecting mistakes is good, but making them impossible is even better. [[Preventive Care]]

Some examples and solutions of eliminating failure cases

- Problem: argument mismatch or wrong order (e.g. arguments pass to 'printf')
  Solution: combine related arguments into one object or use helper function to match formatted string with corresponding field name and passing it to the function call.
  
- Problem: complicate constructor with lots of parameters.
  Solution: use a Param class to set all the params and pass the Param as argument to the constructor. The Param class can implement chaining methods if there are long list of parameters to set. 
  
- Problem: different functions managing the state of an object.
  Solution: the object has a stack which keeps track of all the state changes. A token class will push the stack in its constructor and pop the stack in its destructor. When a function requests a state change of the object, it will create a token. Once it's done or the function ends, the token will be destroyed. 
#### Rule 8 - Code that isn't running doesn't work

Delete orphaned code (code not being called anymore) as soon as possible. You should feel happy about this because you are reducing the amount of code without losing any functionalities. Orphaned code are often a growing bed for bugs.
#### Rule 9 - Write collapsible code

Short-term memory can only handle 7 +/- items at one time. Code reading is a cognitive load and you are basically doing mental juggling. When you can't handle all the items, you will drop some of them and you have no control which one to drop. That's why in your function, you should not have more than 7 (prefer 5) concurrent tracks (including accumulating facts and links or connections).

Abstraction (moving logic into functions) can help collapse details into a single concept. Thus, reducing the number of items to keep track of in the short-term memory. However, there is a cost to abstraction, don't over do it. It adds an extra layer and may obscure what's going on. Use it only if it makes the code more simple and easier to understand.

Always use common concepts, patterns and conventions in your code. Common knowledge is free, but new concepts are expensive. If you have to work on something new or complicated, break it down into small, related chucks that contain familiar concepts. Do this recursively until the whole thing is clear and become manageable. Same goes for learning, building new habits and adapting to a new environment.
#### Rule 10 - Localize complexity

You can't avoid complexity, but you can contain it. Keep the complexity internal and expose a simple interface. Avoid complicate interactions at all cost. 

If adding a new feature involves writing code in a lot of places, that's a bad sign!
#### Rule 11 - Is it twice as good?

As your project hits its limit, you may think that's because the initial design was poor. A better design would have avoided the problem. But this is not going to happen. Predicting the future would only end up with an equally poor, as well as, complicate design, which would also hit its limit soon. ==Futureproofing is very dangerous. Most of the time, it is not necessary and many times it doesn't work.

==Many programmers handle this poorly, making big changes for the wrong reason at the wrong time. Ending up with more problems than they solve.

##### 2 types of programmers:

 Type 1 programmers think about problem in terms of existing solution. They solve problems by tweaking the existing design. They like to make incremental changes.
   
   **Issue with type 1 programmer**
   They may end-up trapped in the existing design and miss out improvements. As time goes by, they will be buried under the weight of tons of tweaks and exceptional cases, making it harder and harder to make changes or add new features.
   
   **Warning signs that you are a type 1 programmer**
   - You describe issue in terms of current architecture or using internal terms, instead of describing it in its own problem space.
   - You tend to use 'impossible' for hard problems. 
   - You use schedule as a conversation-stopper. 
   - It has been a very long time since the last major changes.
   
Type 2 programmers think about problem and solution together. They try to solve all issues with a system, not just the issue at hand. They like to start over with a new design.
   
   **Issue with type 2 programmer**
   Every time is a ground-up rework. They throw out things that contain accumulated knowledge from the previous design. Every new design has its own set of problems and they will never make progress.
   
   **Warning signs that you are a type 2 programmer**
   - Your best reason for the change is  "we really need to clean up this code"
   - Decision is driven by only one particular case.
   - Argument for change is driven by performance issue, but has not done any profiling to identify the bottleneck.
   - Arguments are based on the solution, not the issue at hand.
   - Some bright and shiny new technology is involved.

The best approach is striking a balance between these 2 types of mindset and know when to use them. The question to ask yourself is "Will the result be twice as good?" You will need to do some measurements or estimation (if measure is not possible) to answer this question. Even if it's not easy to quantify the benefits, you should still try to, instead of skipping the question. If you do, you are setting yourself up to make the most comfortable decision, that inclines to your natural tendency. Doing this too often will get yourself in trouble.

Major changes must be justified with major improvements. Don't tear up something and replace it with something just marginally better.
#### Rule 12 - Big teams need strong conventions

Programming is a work of complicity. Your productivity is heavily influenced by that. The more complicated you make things, the less successful you will be. And the opposite is true.

Don't mix styles and conventions in the same project. This adds complexity. There are different styles in error handling and problem solving. Although sticking to one is not always easy, you should do it. Have written rules for all the conventions and stick to them. For example:
- How to name everything
- Where to set file boundaries. How code should be ordered and grouped inside the file.
- Where you define constants.
- Where to store configurations and how they are structured.
- How to do error handling. 

Different types of error handling:
1. Not handling at all. Let the language or framework to take care for you.
2. Have the function named tryXXX() and return a boolean. Details about the error is logged.
3. Return a result object which contains error code, error message and other details of the error.
4. Throw exceptions.
5. Use assert.
#### Rule 13 - Find the pebble that started the avalanche

Things usually go wrong bit by bit, rather than all at once. Thus, debugging is also working backward bit by bit.

Since working backward or finding the root cause is difficult, we tend to just fix the symptoms instead. However, the cause of the original problems still lies somewhere and is poise to cause more troubles.

**Things to make debugging easier:
- Pushing symptoms closer to the cause.
- Reducing the length of causal chain.
- Make it easier to hop back in time.
The last one is the easiest to target, if we can make reproducing the state when the problem occurs easier. Having a lot of states makes debugging more complicate and time consuming. Thus, if we could reduce the amount of states, hopping back the causal chain would be easier. Pure functions without state is easy to debug. 

Use state only if it's absolute necessary. Try to build behavior out of pure functions. However, it doesn't have to be all or nothing, removing every bit of state helps. 

Adding audit function for every state change helps, and this can save you lots of time and tedious work. Another helpful tool is to log all the state changes (or inputs for pure functions) and make the log file executable (or play back the function calls) so you would be able to reproduce the state that leads to the problem.
#### Rule 14 - Code comes in 4 flavors

Simplify view of problems and solutions:

-- | Simple Problem | Hard Problem
-- | -- | --
Simple Solution | Expected | Aspirational
Complicate Solution | Very bad | Accepted

Why do we create complicate solutions for simple problems?
1) Too much abstraction
2) Too much generalization, trying to solve more than it should
3) Using the wrong algorithm, or misunderstanding the problem

Complicate code is harder to read, to write and to debug. They are usually more buggy and slower to run. The programmer doing this is not only making her own job harder, but everyone else on the team.

There are 3 types of programmers

-- | Easy Problem | Hard Problem 
-- | -- | --
Mediocre Programmer | Complicate | Complicate 
Good Programmer | Simple | Complicate
Great Programmer * | Simple | Simple

*A great programmer is someone who can tell a seemingly hard problem is actually easy if considering from the right perspective.
#### Rule 15 - Pull the weeds
See also [[Good Housekeeping]]

Weeds in a project are something that are:
- easy and safe to fix, but also easy to ignore
- when fixed, it shouldn't cause any side effects or problems 
- the fix should make no functional changes
- the fix shouldn't take much time
- the only change is you have 1 less weed

Clearing weeds makes:
- the codebase more pleasant to work with
- makes everyone's job easier
- makes important stuff more visible
#### Rule 16 - Work backward from your result, not forward from your code

Programming is like building a bridge to close a gap. On one side you have a problem, and on the other side you have some pile of code and technologies to work with. Most programmers are standing on the side of their existing code which they know very well and are comfortable with. However, they may know very little about the program they are going to solve.

When you try to solve a problem, are you holding onto some existing solutions and try to tweak it to work for the problem? Or are you standing in the problem and come up with the best solution? If you only have a hammer, every problem is a nail to you.

Try to forget the solution you have for a moment (forget about code reuse). Focus on the problem at hand and come up with the most simple solution. How will you implement the solution?
#### Rule 17 - Sometimes the bigger problem is easier to solve

*"Pick the simplest and most boring approach to every problem you encounter; if you can think of an exciting approach, it's probably a bad idea;"

You should solve specific problem that you understand rather than trying to solve some general problem that you don't. There are times when solving problem with a general solution is the better option. However, this only happens rarely. 

When to consider a general solution:
- the general problem is easier to solve than the specific one
- you have enough examples to be confident that the general problem is worth solving.
- there is a major change in perspective

The general solution represents a completely different way of thinking about the problem. This new perspective allows a radically simpler solution.
#### Rule 18 - Let your code tell its own story

Your code should tell its own story without your narration. This is what you should always aim for.
Ways to make your code easy to read:
- hide behavior with abstractions
- choose good names 
- choose the simplest workable approach
- make your intent obvious

A good comment tells the reader about things that are not obvious. For example:
- explain why the code is written the way it is.
- expected usage for a function.
- part of the code that needs further work.

Code that doesn't run is not working. Same applies to comments which are code that never runs. What they describe may no longer match the function of the code. Solution to this is change comment to assert. 
#### Rule 19 - Rework in parallel

*"For each desired change, make the change easy, then make the easy change."*

When multiple team members are working on the same code, one solution to avoid conflict is to create separate branches and then do merging afterwards. However, this approach can be difficult and time consuming, especially when changes are tightly mingled and wide spread.

Another approach is working in parallel, that is checking in changes on the same branch. For this to work, we have to add a wrapper class and and a switch to turn on/off the new version. This saves the time for doing merging and resolving conflicts. It also makes testing and debugging easier. However, this approach will only work if the old and new version of the code could share the same interface. The changes and the switch hide behind the wrapper class that implement this interface. 
#### Rule 20 - Do the math

Some decisions boil down to simple math and you need to be able to recognize these situations. When there are quantifiable constrains and measurable solutions, it's time to do the math. Remember to take measurements whenever possible, and estimate only when measurements couldn't be done.

==Remember doing the math is to identify solutions that won't work, not to verify that a solution will work.

It's not easy to make decisions when there are trade-offs and soft limits (no clear boundaries). It helps to establish some hard limits to clarify and simplify technical decisions. 

Once you identify hard limits in your problem space or solution, you should respect them from the start of design process. Some examples of hard limits:
- memory constraint
- storage available
- network speed and packet size
- frame rate

Another situation worth doing the math is automation. Automation is an optimization problem. Just like any optimization work, you first need to measure the process before trying to optimize it. Then, identify the cost (that is how much time you will need to implement the automation) and the benefits (how much time you will save with the automation).
If the cost-benefit is a close call, then don't do it. Programmers usually underestimate the time it takes for their work.

When there are changes to the process you want to automate or changes on hard limits, make sure to redo the math.

#### Rule 21 - Sometimes you just need to hammer the nails

Not every problem has an elegant solution. Even the most exciting task has moments of drudgery. The key is to know when the danger signs show up. Knowing the kind of tasks that you tend to put behind is the key to self-knowledge. Once you have this kind of awareness, you can assign proper priorities to these tasks. 

==Half-completed tasks are slow poison, that is going to kill your project.

Often we choose the short and easy path, giving up long term benefits of cleaner and simpler codes.