![OverEngineering](/images/2024-05-11-OverEngineering.jpg)

You might have heard the term "Overengineering" frequently, and many people advise avoiding it during software development. But what is overengineering? How does it creep into software development, and how can we prevent it?

# Overengineering

When developing software from scratch, there are many details to consider at the beginning, and numerous problems to solve during the development process. It's easy and unfortunately common to fall into the trap of overengineering. According to [Wikipedia's definition of overengineering](https://en.wikipedia.org/wiki/Overengineering), if your solution "is complicated in a way that provides no value" or "could have been designed to be simpler," you've overengineered.

# Examples of Overengineering

Let's delve into this definition with some examples. Imagine you're building a todo app. A basic version of this app would allow users to create a todo, list all todos, and mark a todo as done. The trap of overengineering appears here. You might start thinking about features like categorizing todos, adding subtasks, attaching files and multimedia to a todo item, or sharing todos with other users. While these features might be useful in future iterations, for the initial todo list app, they create unnecessary complexity and provide no immediate value. Overengineering like this increases time to market and, in the worst-case scenario, might cause the entire project to fail.

Suppose you've decided to go with a simpler version of the app. You start with a complex architecture, such as [Hexagonal Architecture](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)). These types of architectural design patterns are introduced to simplify complex businesses, but the app you want to develop is straightforward and could be done with less than 100 lines of code. By introducing architectural design patterns, you're actually complicating a simple business!

Then, after building the app, you have to decide how to deploy it. You could start with a simple serverless approach in AWS or create a Kubernetes cluster. The second approach might make the app capable of handling millions of active users per day. But do you really have millions of active users, or will you have to wait months for the first 1000 users? Do you really need this complexity? I don't think so.

These are just some examples of overengineering. I'm not saying that all these features are unnecessary, but they can wait for future iterations. I'm not suggesting that you don't need architectural design patterns. But when the app is growing and adding new features becomes cumbersome, then you can refactor and add architectural design patterns to manage the increasing complexity. I'm not saying you'll never have to handle lots of concurrent active users. In fact, I hope you someday face this challenge. But you can start with a simpler and cheaper solution and then scale the app when necessary.

# How to Avoid Overengineering?

It might seem challenging to avoid the trap of overengineering, but it's quite simple! You just need to ask two straightforward questions for each decision you make: "Does it provide value to the users?" and "Does it simplify things?" If the answer to both questions is "No," then you should not proceed with the decision. If both answers are "Yes," then it's the right way. When one question's answer is "Yes" and the other's is "No," there might be another solution. You just need to dig deeper to find it!