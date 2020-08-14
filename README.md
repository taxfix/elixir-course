The content of the Elixir course is covered by the **Creative Commons (by-nc-sa)** https://creativecommons.org/licenses/by-nc-sa/4.0/
![License CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc/4.0/88x31.png)

# Elixir course

![images/the-simpsons.png](images/the-simpsons.png)

This course is an **asynchronous** course that it is running in
![Taxfix](https://taxfix.de/en/) to give the opportunity to developers who are
not (yet) confident to Elixir to power up their skills.

This course, is also an open to contribution course! We decided to open it to
everyone to give back to the Elixir community. 👐

We are also sharing the slides of the talk ![Drinking a little bit of Elixir](talk/Drinking-a-little-bit-of-elixir.html.tar.gz)
that was delivered to initiate this Elixir course.

## Episode 0

![images/lisa-yoga.jpg](images/lisa-yoga.jpg)

(***Endtroducing...)*** 

🎶 [https://www.youtube.com/watch?v=FGQjrBuW-Xg&list=OLAK5uy_lA4P3neYe5g7f9Vs7VD0oCYHcEPytjupI](https://www.youtube.com/watch?v=FGQjrBuW-Xg&list=OLAK5uy_lA4P3neYe5g7f9Vs7VD0oCYHcEPytjupI)

Hello everyone! 👋🏿

This is an hands-on Elixir Course for you folks, that are curious or already looking into learning and contributing to the Elixir ecosystem.

The scope of this course is **not** to teach you how to do:

```elixir
iex> 1 + 1
2

iex> IO.puts "Hello Elixir world!"
"Hello Elixir world!"
```

Ops, we already did it! 😇

Instead, you as coders can independently check the elixir documentation and skim through the basics.

But let's step back and do an **introductory** **TL;Do Read** section!

**Before talking about Elixir, we should talk about…**

### **Erlang**

Because Elixir has vintage roots.. for instance **Erlang was created in** **1987** and we have to know our **past** to know the **future** (or better, the **present**!) So..

### Erlang is the “father” of Elixir

**And by definition..**

Erlang is a programming language used to build massively scalable soft real-time systems with requirements on high availability. Some of its uses are in telecoms, banking, e-commerce, computer telephony and instant messaging. Erlang’s runtime system has built-in support for concurrency, distribution and fault tolerance. Erlang runs on the **BEAM**

### mmm.. so… What is the `BEAM`?

The **BEAM** is the virtual machine at the core of the Erlang **Open Telecom Platform** (OTP). **BEAM** is part of the Erlang Run-Time System (ERTS), which compiles **Erlang**, **Elixir**, **Lisp Flavoured Erlang (LFE)** (and more..) source code into bytecode, which is then executed on the BEAM

### What about Elixir?

Elixir is a child language of Erlang that runs on the BEAM

### More formally, Elixir is…

…a dynamic, functional language designed for building scalable and maintainable applications.

**Elixir** leverages the **BEAM** (Also called sometimes **Erlang VM**), **known for running low-latency, distributed and fault-tolerant systems**, while also being successfully used in web development and the embedded software domain.

### Elixir is an immutable and functional language focused on concurrency

You can pass state from a function to another, however if you have the need to keep state in memory how you do it?

### You can...

"Assign" the result of the function to a variable! For example let's assume that we have an *append* function that puts at the end of a list an element:

```elixir
iex> my_list = [] # "Assign" or bind an empty list to my_list variable
[]
iex> append(my_list, 1) # appends but not "assigns" to a variable
[1]
iex> my_list
[]
iex> my_list = append(my_list, 1) # Append to my_list "1" and assigns
[1]
iex> my_list # Check if the value is there
[1]
```

### But.. there's another way!

### So, let’s talk about processes…

In Elixir, all code runs inside processes. Processes are isolated from each other, run concurrent to one another and communicate via message passing.

Processes are not only the foundation for concurrency in Elixir, however they also provide the building blocks for constructing distributed and fault-tolerant systems.

Bear in mind that processes are **NOT** always necessary even if they are very **cheap** to create. You can create thousands or millions of them very quickly. *As an example*, a process in Elixir can be compared to the speed of checking out a new git branch.

If you are curious about **when** processes **can be used** check this out [https://hexdocs.pm/elixir/master/library-guidelines.html#avoid-using-processes-for-code-organization](https://hexdocs.pm/elixir/master/library-guidelines.html#avoid-using-processes-for-code-organization) (**hint:** **read it** ;) )

### Tasks

Tasks are a way of achieving concurrency in Elixir, and follow a similar async/await pattern like in other languages. Ideally you don't want to be communicating with other processes from inside the task, as this can get messy and lead to things like deadlock. Instead the approach that is usually taken for more complex tasks, is to use a GenServer.

With this in mind, there are use cases for Tasks, so it's worth having a read about them [https://hexdocs.pm/elixir/Task.html](https://hexdocs.pm/elixir/Task.html). 

### GenServer

Whenever you read about Elixir, you're sure to read about GenServers. GenServers are nothing more than a process that implements a basic client-server behaviour and allows you to run tasks asynchronously and store state. GenServers contain a mailbox where they store their incoming messages and process them as they come. Due to this, it's better to have multiple GenServers if possible rather than just one, as GenServers can quickly become a bottle neck for your application. It's totally acceptable (and expected) that you could have one (or more) GenServers per user. 

Developers new to the language can be quick to jump to conclusions about a problem, and start using GenServers everywhere. In practice, it's better to only use GenServers when you really need them (e.g storing state and working on that state). If you don't need a GenServer, don't use one. Just because it's an Elixir program, doesn't mean it needs a GenServer.

In cases where you just want to store state, and access and update it. It's worth looking into Agents.

### OTP (Open Telecom Platform)

**OTP** is a collection of useful **middleware, libraries, and tool**s written in the **Erlang programming language**. It is an integral part of the open-source distribution of Erlang. The name **OTP** was originally an acronym for **Open Telecom Platform**, which was a name for marketing  before **Ericsson** released **Erlang/OTP as open source**. However neither **Erlang** nor **OTP** are specifically designed to build **telecom applications only**.

Keep in mind that **Erlang/OTP** and **Elixir** they give you the **lego block**s to build fault tolerant distributed systems, however creating distributed systems does not come for free with **OTP.** Although compared to other programming languages you get a rich ecosystem to reach this goal! (creating distributed systems)

### Let’s go back to talk about the BEAM (The Erlang Virtual Machine)

On the **BEAM** you **don’t have an event loop**. The way the **BEAM** handles **pre-emption** is through reductions.

### So, when you have a faulty process…

….that is consuming a lot of CPU, the rest of the processes will run without impact and smoothly.

Being the **BEAM pre-emptive**, it introduces **stability** to the system and especially **predictability**.

If designed well, a system thru-put is predictable even if you have a high load.

### Garbage collection

**Garbage Collection** is different from virtual machines like the **JVM**. Garbage Collection is applied **per process** and you don’t have big Garbage Collector **pauses.**

### Happy path programming

With OTP at your disposal, you can program in a non-defensive way. **In certain cases you want that,** if there is a fault in one of your processes, you want to let it crash (or restart) to clean its state. In some cases you would want a process to crash (due to an unexpected error) and restore its state. There are techniques to do this, however you would have to pay attention to avoid to restore a corrupted state.

The gist of the "let it crash" philosophy is that you can't handle all the possible ways of generating exceptions. There will be always an exception that we did not think about, so a **Supervisor process** will take care to **restart** a **crashed process** with a **specific strategy** that you can **specify case by case**.

Surprisingly for many programmers Erlang and Elixir have **exceptions handling**, however they are usually used in **critical parts of the code**. Especially in **IO handling.**

**Not you will dive into episodes that will give you a taste of Elixir!**

## Suggestions on how to approach the course..!

As you write code in a new programming language some people are the **retype code folk** to train muscle memory or the **copy&pasta** **folk** and understand after what you did, etc...

**Choose your style!**

It's **not** important to be **quick** to **finish, it's not a race! ;)**

**Take your time to understand what you are doing.**

Check the **Elixir** **documentation**, try to go **deep**, but **don't** get **lost**! ;)

### Links to check:

- **The official Elixir tutorial:** [https://elixir-lang.org/getting-started/introduction.html](https://elixir-lang.org/getting-started/introduction.html)
- **Elixir School**, **a very good resource** to quickly catch up with Elixir details [https://elixirschool.com/en/](https://elixirschool.com/en/)
- **The Elixir documentation** (check this out when you have any doubt!) [https://hexdocs.pm/elixir/Kernel.html](https://hexdocs.pm/elixir/Kernel.html)
- **The Elixir Forum** is a super good resource to find answers or participate in (**public**) conversations [https://elixirforum.com/](https://elixirforum.com/)
- Comparison of Erlang Runtime System and Java Virtual Machine (you might even learn about java 🙀) [https://pdfs.semanticscholar.org/aeee/adf0c2a2dc453c0e9ef18a0239e9e796e497.pdf?_ga=2.69208912.1940899817.1594286572-947597467.1594286572](https://pdfs.semanticscholar.org/aeee/adf0c2a2dc453c0e9ef18a0239e9e796e497.pdf?_ga=2.69208912.1940899817.1594286572-947597467.1594286572)

## Episode 1

![images/homer-burger.png](images/homer-burger.png)

***(Wet your appetite..!)***

🎶 [https://www.youtube.com/watch?v=265H5xRr4Tc](https://www.youtube.com/watch?v=265H5xRr4Tc)

You will build a **small textual game** in **Elixir**, inspired from a **puzzle game** from **Valve** ([https://en.wikipedia.org/wiki/Portal_(video_game)](https://en.wikipedia.org/wiki/Portal_(video_game)))

You will start to experiment with basic **Elixir** syntax through the **iex** **REPL**

- Learn basic **pattern matching**
- How to create **anonymous functions**
- You will learn that in **Elixir** there are just **modules** and **functions**
- How use the **built-in Elixir code formatter**
- What is an **Elixir protocol**
- You will learn about the **Supervisor** *OTP* *behaviour* and how to **start dynamically processes** and *Supervision trees*
- You will understand how to store state in a process (By using the Elixir **Agent** *behaviour*) and **transfer** the state of a **process** to **another process** in two different local **erlang nodes** running on your laptop.
- If you would have the **ip address of someone** else you could create also an **erlang mesh** between two **remote laptops**!

Start from here and take your time! [https://howistart.org/posts/elixir/1/](https://howistart.org/posts/elixir/1/)

## Episode 2

![images/homer-nirvana.jpg](images/homer-nirvana.jpg)

***(Sailing the seas of functions)***

🎶 [https://www.youtube.com/watch?v=xFinPHgLUXc](https://www.youtube.com/watch?v=xFinPHgLUXc)

**In this episode** after **holistically** 🧝🏿‍♀️ **wetting our appetite** with the **portal game**, we'll **fallback** to only plain **Modules** and **functions.**

**We think that having a good command** of **Modules** and **functions** will **help you** to reason about code (**without** thinking about **processes** from the start)

As aforementioned in the introduction, processes are super cheap to create in erlang/elixir, however they are **not meant** to be **considered** **like objects** in the **OOP sense.**

You could **refresh** this concept by skimming again through [https://hexdocs.pm/elixir/master/library-guidelines.html#avoid-using-processes-for-code-organization](https://hexdocs.pm/elixir/master/library-guidelines.html#avoid-using-processes-for-code-organization)

To dive in the **seas of functions** (and **Modules**!) we will use [https://exercism.io/](https://exercism.io/)

**Exercism** let you learn a **new language** (not only **Elixir**!) through small challenges tackling different problems. Some challenges are easy, fun, and relaxing. Some are a tougher. But you can choose what do you want to do.

Every challenge has a **set of failing tests** that you have to make it **successfully pass** by **gradually implementing the solution** (or in **one shot if you are very brave!**)

**Everyone** in an **exercism team** can **review** the **solution** to a **challenge** of the i**nsert coin team** or get **inspired** by **other insert coin team members solutions**

### **Use this link to use to join the "insert coin" exercism team and choose the "Free form Track"**

[https://teams.exercism.io/teams/NDQGCdvzZkK56nfMtNVqWdYg/join](https://teams.exercism.io/teams/NDQGCdvzZkK56nfMtNVqWdYg/join)

## Episode 3

![https://i.kinja-img.com/gawker-media/image/upload/c_scale,f_auto,fl_progressive,pg_1,q_80,w_800/qkawdwisdh71ssnzzgn9.jpg](https://i.kinja-img.com/gawker-media/image/upload/c_scale,f_auto,fl_progressive,pg_1,q_80,w_800/qkawdwisdh71ssnzzgn9.jpg)

🎶 [https://www.youtube.com/watch?v=D_8Pma1vHmw](https://www.youtube.com/watch?v=D_8Pma1vHmw)

### Releases

Now that we know how to build a basic project, we need to know how to release it. Historically releases have been a bit of a pain in Elixir, but luckily for you, the newer versions of the language come with a built in task! 

[https://hexdocs.pm/mix/Mix.Tasks.Release.html](https://hexdocs.pm/mix/Mix.Tasks.Release.html)

Mix release offers us a very quick way to build a release of our application. However, if you've decided to get fancy with your applications and build applications that are stateful, it's worth spending some time learning about Hot code releases in Elixir, as well as a tool called Distillery, which helps to support this. 

[https://hexdocs.pm/distillery/home.html](https://hexdocs.pm/distillery/home.html)

## Season break!

[images/tumblr_ns2v6ccj521sg05bjo4_500.webp](images/tumblr_ns2v6ccj521sg05bjo4_500.webp)

🎶 [https://youtu.be/MWH3h5LdkxA](https://youtu.be/MWH3h5LdkxA)

On this special episode we are going to review what we have learned so far by building a version of the Conway's Game of Life.

The [Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) is a zero-player game, which means that it requires no player interacting with it.

The original setup consists of an infinite, 2-dimensional grid of cells, and each cell can be `alive` or `dead`. At each step of time (`tick`), the following rules apply to decide what happens with each cell.

1. Any live cell with fewer than two live neighbours dies, as if by underpopulation.
2. Any live cell with two or three live neighbours lives on to the next generation.
3. Any live cell with more than three live neighbours dies, as if by overpopulation.
4. Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

And it looks something like the following (but this is a finite 2d grid)

[https://camo.githubusercontent.com/aa8c99f5cf763884b878f700807539aa56dba266/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f652f65352f476f73706572735f676c696465725f67756e2e676966](https://camo.githubusercontent.com/aa8c99f5cf763884b878f700807539aa56dba266/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f652f65352f476f73706572735f676c696465725f67756e2e676966)

And ours will look more like this (just the looks, it is not actually following any of the rules).

![https://github.com/ggpasqualino/workshop-elixir-game-of-life/raw/main/docs/dynamic-game.gif](https://github.com/ggpasqualino/workshop-elixir-game-of-life/raw/main/docs/dynamic-game.gif)

### Bot Project

For this project we want you to build a basic bot using Hedwig ([https://github.com/hedwig-im/hedwig](https://github.com/hedwig-im/hedwig)). Hedwig provides the basic framework for setting up your application, so you can follow the instructions on the GitHub page to get started. You're totally free to decide what you'd like your Bot to do, some examples of things that have been done before can be found here [https://github.com/enilsen16/awesome-hedwig](https://github.com/enilsen16/awesome-hedwig). 

## Episode 4

![https://media1.tenor.com/images/3e0fe1635ecd36113734082ceffe6ace/tenor.gif](https://media1.tenor.com/images/3e0fe1635ecd36113734082ceffe6ace/tenor.gif)

🎶 [https://www.youtube.com/watch?v=16y1AkoZkmQ](https://www.youtube.com/watch?v=16y1AkoZkmQ)

### Erlang Term Storage (ETS)

ETS is a storage system built into OTP that allows us to store Elixir and Erlang objects directly and offers constant time access. You can think of ETS as a caching mechanism, as the tables are killed if you take the application down. If you want something similar to ETS that offers longer term storage it's worth looking into dets or mnesia.

### Ecto

Ecto is a database wrapper that is widely used in the Elixir community. For version 3 Ecto was split into 2 different libraries, :ecto and :ecto_sql. :ecto_sql is required if you intend on working with a database, otherwise you can just use :ecto to create schemas (schemas that don't back up to a database are called embedded_schemas) and take advantage of the validation opportunities that it provides. 

### Phoenix + Phoenix Live View

Phoenix is to Elixir what Rails is to Ruby, arguably Phoenix has been one of the greatest draws for people to the Elixir community. Phoenix offers all that you would expect from a framework such as Rails or Django, but has the advantage of being easily scalable as well as being easily able to achieve concurrency due to being built on top of Elixir. 

Phoenix Live View is a relatively new addition to Phoenix, and enables users to create server rendered templates that can compete with the likes of React by being able to send partial state updates to the user. Compared to other frameworks where whenever an update happens, the entire page is sent, Phoenix Live View offers incredible performance as well as ease to setup and get started with. Take a look at the video below to get an idea of what you can achieve with Phoenix and Phoenix LiveView. 

[![Phoenix LiveView](https://img.youtube.com/vi/MZvmYaFkNJI/0.jpg)](https://www.youtube.com/watch?v=MZvmYaFkNJI)

### Project Suggestions + Ideas

For the final stage in the course we'd like you to create your own project that takes advantage of Phoenix + Ecto. There's no other requirements, other than to use these two libraries (if you install Phoenix, Ecto comes included 😉). Phoenix Live View is also worth taking a look into, as it can help save you from writing any JavaScript in your project. Check out the following video to get an idea of what you can achieve with Live View.

Project Ideas (they are just proposals)

- **Markdown Editor -** Build a site that has two panes, on one side you write markdown and on the other side it automatically renders it.
- **Job Scheduler -** Build an application where you can define various background tasks, and then create an interface to see the progress of your tasks, as well as being able to start, restart and pause a task. For task management you could use GenServers or take a look into a library called Quantum.
- **Chat Application -** Take advantage of Phoenix's great websocket support and create a chat application that allows multiple people to talk across various channels. If you want to take it further you could support message history and private messaging between users.
