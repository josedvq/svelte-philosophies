# svelte-philosophies

Based on [react-philosophies](https://github.com/mithi/react-philosophies)

> You have to think about what is the right way, even when you have the right idea of what the building blocks should be, there is huge flexibility in how you decide to put the whole system together. It is a craft... and it has a lot to do with valuing simplicity over complexity. Many people do have a tendency to make things more complicated than they need to be... The more stuff you throw into a system, the more complicated it gets and the more likely it is not going to work properly. - Barbara Liskov


## 🧘 0. Introduction

`svelte-philosophies` is:
- things to think about when writing `svelte` code.
- at the back of my mind whenever I review someone else's code or my own
- just guidelines and NOT rigid rules
- a living document and will evolve over time as experience grows
- mostly techniques which are variations of basic [refactoring](https://en.wikipedia.org/wiki/Code_refactoring) methods, [SOLID](https://en.wikipedia.org/wiki/SOLID) principles, and [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming) ideas...


## 🧘 1. Coding principles

### 1.1 Recognize when the computer is smarter than you

1. Statically analyze your code with [`ESLint`](https://eslint.org/). 
2. Enable ["strict"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) mode. It's 2022. 
8. There is a reason why errors and warnings are displayed in the console.
10. [Prettier](https://prettier.io/) (or an alternative) formats your code for you, giving you consistent formatting every time. You no longer need to think about it!
11. [`Typescript`](https://www.typescriptlang.org/) and frameworks such as [`NextJS`](https://nextjs.org/) make your life so much easier.
12. I highly recommend [Code Climate](https://codeclimate.com/quality/) (or similar) for open-source repositories or if you can afford it. I find that automatically-detected code smells truly motivates me to reduce the technical debts of the application I'm working on!

### 1.2 Code is just a necessary evil

> "The best code is no code at all. Every new line of code you willingly bring into the world is code that has to be debugged, code that has to be read and understood, code that has to be supported." - Jeff Atwood

> "One of my most productive days was throwing away 1000 lines of code." - Eric S. Raymond

See also: [Write Less Code - Rich Harris](https://svelte.dev/blog/write-less-code), [Code is evil - Artem Sapegin](https://github.com/sapegin/washingcode-book/blob/master/manuscript/Code_is_evil.md)

#### 1.2.1 Think first before adding another dependency

Needless to say, the more you add dependencies, the more code you ship to the browser. Ask yourself, are you actually using the features which make a particular library great?


#### 1.2.2 Don't be clever. YAGNI!

> "What could happen with my software in the future? Oh yeah, maybe this and that. Let’s implement all these things since we are working on this part anyway. That way it’s future-proof."

**Y**ou **A**ren't **G**onna **N**eed **I**t! Always implement things when you actually need them, never when you just foresee that you may need them. The less code the better! ([Martin Fowler: YAGNI](https://martinfowler.com/bliki/Yagni.html), [C2 Wiki: You Arent Gonna Need It!](https://wiki.c2.com/?YouArentGonnaNeedIt))

Related section: [2.4 Duplication is far cheaper than the wrong abstraction](#-24-duplication-is-far-cheaper-than-the-wrong-abstraction)

### 1.3 Leave it better than you found it

**1.3.1 Detect code smells and do something about them if you need to**. 

If you recognize that something is wrong, fix it right then and there. But if it's not that easy to fix or you don't have time to fix it at that moment, at least add a comment (`FIXME` or `TODO`) with a concise explanation of the identified problem. Make sure everybody knows it is broken. It shows others that you care and that they should also do the same when they encounter those kinds of things.

Examples of easy-to-catch code smells:
- ❌ Methods or functions defined with a large number of arguments
- ❌ Boolean logic that may be hard to understand
- ❌ Excessive lines of code within a single file
- ❌ Duplicate code which is syntactically identical (but may be formatted differently)
- ❌ Functions or methods that may be hard to understand
- ❌ Classes / Components defined with a large number of functions or methods
- ❌ Excessive lines of code within a single function or method
- ❌ Functions or methods with a large number of return statements
- ❌ Duplicate code which is not identical but shares the same structure (e.g. variable names may differ)


Keep in mind that code smells don't necessarily mean that code should be changed. A code smell just informs you that you might be able to think of a better way to implement the same functionality.

**1.3.2 Merciless Refactoring. Simple is better than complex.**

> Is the CL more complex than it should be? Check this at every level of the CL—are individual lines too complex? Are functions too complex? Are classes too complex? “Too complex” usually means “can’t be understood quickly by code readers.” It can also mean “developers are likely to introduce bugs when they try to call or modify this code.”- [Google Engineering Practices: What to look for in a code review](https://google.github.io/eng-practices/review/reviewer/looking-for.html)


**💁‍♀️ TIP: Prefer chained higher-order functions over loops**

If there is no discernable performance difference and if possible, replace traditional loops with chained higher-order functions (`map`, `filter`, `find`, `findIndex`, `some`, etc) [Stackoverflow: What is the advantage of using a function over loops?](https://stackoverflow.com/questions/34402198/what-is-the-advantage-of-using-a-function-over-loops)


### 1.4 You can do better


**💁‍♀️ TIP: Think about how your component will be used before coding it**

[Writing APIs is hard](http://sweng.the-davies.net/Home/rustys-api-design-manifesto). [`README Driven Development`](https://tom.preston-werner.com/2010/08/23/readme-driven-development.html) is one useful technique to help design better APIs.  I'm not saying we should [RDD](https://rathes.me/blog/en/readme-driven-development/) religiously, just saying that the idea behind it is great. I find that when I first write the API (how the component will be used) before implementing it, this usually creates a better designed component than when I don't.

## 🧘 2. Design for happiness - architecture principles

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." - Martin Fowler

> "The ratio of time spent reading versus writing is well over 10 to 1. We are constantly reading old code as part of the effort to write new code. So if you want to go fast, if you want to get done quickly, if you want your code to be easy to write, make it easy to read." ― Robert C. Martin [(Not saying I agree with his political views)](https://www.getrevue.co/profile/tech-bullshit/issues/tech-bullshit-explained-uncle-bob-830918)

> Premature optimization is the root of all evil - Tony Hoare 

**TL;DR**

1. 💖 Find the right shape for your state. 
2. 💖 Find the right home for your state. State in svelte can live locally (component state), globally, or in between (in a context). 
2. 💖 Avoid state management complexity by removing redundant states
3. 💖 Pass the banana, not the gorilla holding the banana and the entire jungle (prefer passing primitives as props)
4. 💖 Keep your components small and simple - the single responsibility principle!
5. 💖 Duplication is far cheaper than the wrong abstraction (avoid premature / inappropriate generalization)
6. Avoid prop drilling by using composition ([Michael Jackson](https://www.youtube.com/watch?v=3XaXKiXtNjw)). `Context` is not the solution for every state sharing problem
7. Split giant `useEffect`s to smaller independent ones ([KCD: Myths about useEffect](https://epicreact.dev/myths-about-useeffect))
8. Consider extracting complex logic to helper objects/functions 
9.  `Context` does not have to be global to your whole app. Put `Context` as low as possible in your component tree. Do this the same way you put variables, comments, states (and code in general) as close as possible to where they're relevant / being used. [Principle of the lowest common ancestor](https://michaelnthiessen.com/first-principle-of-state-management)
10. Keep an eye on the latest frameworks and the ideas behind them [Stackoverflow trends](https://trends.stackoverflow.co/?tags=angularjs,angular,reactjs,svelte,vuejs3,vue.js,next.js) is useful for this.


### 💖 2.1 Find the right shape for your state. 
State that changes together should live together. Group state in a class and describe each variable or use clear names for state variables.

This makes it easier to follow 

### 💖 2.1 Avoid state management complexity by removing redundant states

When you have redundant states, some states may fall out of sync; you may forget to update them given a complex sequence of interactions.
Aside from avoiding synchronization bugs, you'd notice that it's also easier to reason about and require less code.
See also: [KCD: Don't Sync State. Derive It!](https://kentcdodds.com/blog/dont-sync-state-derive-it), [Tic-Tac-Toe](https://epic-react-exercises.vercel.app/react/hooks/1)


### 💖 2.2 Pass the banana, not the gorilla holding the banana and the entire jungle

> You wanted a banana but what you got was a gorilla holding the banana and the entire jungle. - Joe Armstrong

To avoid falling into this trap, it's a good idea to pass mostly primitives (`boolean`, `string`, `number`, etc) types as props. (Passing primitives is also a good idea if you want to use `React.memo` for optimization)

> A component should just know enough to do its job and nothing more. As much as possible, components should be able to collaborate with others without knowing what they are and what they do.

When we do this, the components will be more loosely coupled, the degree of dependency between two components will be lower. Loose coupling makes it easier to change, replace, or remove components without affecting other components. [stackoverflow:2832017](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)

    
Notice that in the `✅  "better" solution"`, `SeeMore` and `Summary` are components that can be used not just by `Member`. It can be used perhaps by other objects such as `CurrentUser`, `Pet`, `Post`... anything that needs those specific functionality.

### 💖 2.3 Keep your components small and simple

**What is the single responsibility principle?**

> A component should have one and **only one** job. It should do the smallest possible useful thing. It only has responsibilities that fulfill its purpose.

A component with various responsibilities is difficult to reuse. If you want to reuse some but not all of its behavior, it's almost always impossible to just get what you need. It is also likely to be entangled with other code. Components that do one thing which isolate that thing from the rest of your application allows change without consequence and reuse without duplication.

**How to know if your component has a single responsibility?**

> Try to describe that component in one sentence. If it is only responsible for one thing then it should be simple to describe. If it uses the word ‘and’ or ‘or’ then it is likely that your component fails this test.

Inspect the component's state, the props and hooks it consumes, as well as variables and methods declared inside the component (there shouldn't be too many). Ask yourself: Do these things actually work together to fulfill the component's purpose? If some of them don't, consider moving those somewhere else or breaking down your big component into smaller ones.


> Not only should a component have a single responsibility, it should also have a clear spot on the spectrum of abstraction. On one end, we have generic building blocks like `<Button>`, `<Heading>`, `<Modal>`. On the other end, we have one-off templates like `<Homepage>` and `<ContactForm>`. Every component should have a clear spot on this spectrum. A `<Button>` component shoudn't have a _user_ prop, since users are a higher-abstract concept and `Button` is a low-abstract component.


### 💖 2.4 Duplication is far cheaper than the wrong abstraction

Avoid premature / inappropriate generalization. If your implementation for a simple feature requires a huge overhead, consider other options.
I highly recommend reading [Sandi Metz: The Wrong Abstraction](https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction).

> A particular type of complexity is over-engineering, where developers have made the code more generic than it needs to be, or added functionality that isn’t presently needed by the system. Encourage developers to solve the problem they know needs to be solved now, not the problem that the developer speculates might need to be solved in the future. The future problem should be solved once it arrives and you can see its actual shape and requirements in the physical universe. - [Google Engineering Practices: What to look for in a code review](https://google.github.io/eng-practices/review/reviewer/looking-for.html)

See also: [KCD: AHA Programming](https://kentcdodds.com/blog/aha-programming), [C2 Wiki: Contrived Interfaces](https://wiki.c2.com/?ContrivedInterfaces)/[The Expensive Setup Smell](https://wiki.c2.com/?ExpensiveSetUpSmell)/[Premature Generalization](https://wiki.c2.com/?PrematureGeneralization)


6. Putting your state as close as possible to where it's being used will not only make your code so much easier to read but it would also make your app faster (state colocation)
7. `Context` should be logically separated, do not add too many values in one context provider. If any of the values of your context changes, all components consuming that context also rerenders even if those components don't use the specific value that was actually changed.



        

(Note, the above is taken from his response to my email... I really appreciate that he took the time to share his ideas 🙂)
