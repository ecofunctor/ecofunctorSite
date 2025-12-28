+++
author = "Eason"
date = 2025-12-11
title = "7 years of Scala religion: From backend to chip design"
image = "/images/hardangervidda.jpg"
+++

I'm Eason du, a Scala enthusiast for many years. This is the first part of my story of using Scala for 7 years. I'm writing this story just before the upcoming Scala meetup. This post is causally written, as a mixture of my Scala career, thoughts about Scala, and some life experiences, so please forgive me for lack of clearness and read it causally.

## From Haskell to Scala
I started using Scala in 2018, when I graduated from college as Bachelors. My journey with programming started from high school with C for embedded systems, and I continued with Java for Android development just before college. I become interested in functional programming and programming language theory after reading the book "Hackers and Painters" by Paul Graham, which mentioned Lisp. So I started to use Lisp to do homework assignments in college. Later I found Haskell, and I was fascinated by its elegance and mathematical beauty. So I switched to Haskell and used it for most of my homework assignments wherever possible. Then it's time to graduate, and when I was looking for jobs, it seemed that the chances of getting a job with Haskell is very low. My first job is full stack development with Java and Typescript, and during that time, I learned about Kotlin and Scala, and after trying both, I decided to invest in Scala, since it feels more functional.

Then I'm lucky to get a job about Scala backend development with Akka. I still remember it's not easy to grasp Scala and it's ecosystem at the beginning, due 
to the complexity of Akka framework, maybe taking me almost half a year to be confident in it. In this process, I'm also quite excited to learn new concepts  everyday, such as Akka actors, clustering, streams, etc.

Retrospectively, I think I have the almost ideal background for Scala, Since I write both Haskell and Java(and Scala = Java + Haskell). Since then, I have been using Scala for almost everything, including work projects, open source projects, and personal projects. 

## From backend and big data to chip design
It's extremely lucky that I'm able to use Scala all over my career(one reason is that Scala is at the most popular time during these years for internet companies). Another reason is that I'm obsessed with applying functional programming in my work, and I feel painful when I have to use other languages like Java, Python, or C++. To keep using Scala, I have jumped between different domains, from backend services, to big data, to chip design(compiler), and to AI. I can't imagine to work in so many fields if I'm not using Scala. 

I didn't see any of my friends or colleagues to do that, and I think the reasons are:
- functional programming is very general, and Scala is the most practical functional programming language
- Due to the first point, Scala is applicable to many domains
- Skills in Scala in one domain is transferable to another domain
- Using Scala let me unify different knowledge in different domains, so I can learn faster

## Returning to China in 2025
After working in Norway for 2 years where I mainly used Scala for big data and Spark, I returned to China and started as a research assistant about chip design with Chisel, a Scala based DSL for chip design. More specifically, our group is working on formal verification of chip design. And again, formal verification is a field that is very close to functional programming, so I'm able to continue my Scala journey, and deepen my understanding of functional programming and mathematics to a new level after my math-intensive study in DTU, Denmark.

The local community of Scala in China has shrinked a lot from 2023 when the biggest sponsor Tubi freezed hiring and stopped organizing meetups, due to the recent layoffs in tech industry, so it's difficult to gather more Scala enthusiasts together. There are also multiple reasons:
- People usually use whatever language is mandated by their job, and that's usually not Scala
- People that previously used Scala are forced to switch to other languages due to job change or project change
- Many internet companies have finished their development, and not much new development is needed, so the demand for backend and big data engineers in general has decreased

## Scala in new fields: Chip design, Compilers, AI
I'm optimistic about Scala, and I see its rising and falling as a natural cycle. The rise due to backend and big data might be over, but the new applications in AI and DSLs are just starting.  A recent talk with the author of ScaIR, a Scala library for MILR, shows the potential of Scala in compiler, which is the natural area for functional programming, but currently dominated by C++ due to historical reasons. The rise of the Chisel DSL for chip design implies the potential of Scala in compilers as well, where the expressiveness matters a lot.

Another thought is that, I have often heard the opinion that the new version of xx language is coming and copying the features of Scala(or other functional programming languages), such as Kotlin, Swift, C++, etc, so that those functional programming languages like Scala will be replaced. That didn't happen, and I don't think it will happen in the future. I think one of the reasons is that Scala and other fp languages like Haskell have a relatively graceful theoretical foundation, and it's impossible to copy that beautiful core, but only some superficial features. Thus, those new languages will never fully replace Scala or Haskell, but rather coexist with them.

For career path planning, The choice of programming language is almost never be the decisive factor for most people, but for me, Scala has been the key to open many doors due to my religious belief in it. I'm honored to say that I'm working almost exclusively in Scala for so many years, and I didn't foresee any change to that. This is one reason why the title contains "religion".

Another reason for the word "religion" in the title is that, the prevalence of one programming language probably depends on a lot on the taste of the people that controls the resources(capital, money, personal influence and connections, etc). Thus, the popularity of one language is not decided purely by scientific factors. Based on this reasoning, Another way is to enter business world with Scala, or on the contrary, break down the commercial world with Scala based open source projects, This is relevant to my future plans, where I want to do something, but not in a commercial way.

## Scala js
One more thing I want to mention is Scala js. I have a side project that have very complex frontend logic, and initially I use plain javascript(ES6). With the best js ide at that time(Webstorm), I still feel painful since it's dynamically typed. So I tried Typescript, whose type system is powerful, but typing is optional, and I have the feeling that the type system is not sound enough(practically). Then I also tried Ocaml js (BuckleScript), which has a sound type system, but the IDE support is not great(Have to use Emacs). Finally I saw Scala js, I remember it's version is 0.6.x at that time, and I tried it with IntelliJ IDEA. Amazingly, the IDE support is on par with Scala jvm, and it's like I'm working on Scala jvm. The easy integration with existing js libraries is also great. The only drawback is the large output size, but it's acceptable after optimization and compression. There's also the best UI library Laminar, which feels very elegant and beats React without any doubt. So Scala js has also been my choice for frontend related work since then.

## Ending
In the end, I want to thank all the people that contributed to Scala community. I read lihaoyi's blog posts where he shared his experience from the very beginning of Scala back in 2004([12 years..](https://www.lihaoyi.com/post/12yearsofthecomlihaoyiScalaPlatform.html)), when the Scala ecosystem was much less "batteries included" than now. Nowadays, it's much easier to use Scala for almost everything(except things that prohibit garbage collection). In addition to technical blogs about Scala, I would also enjoyed a lot from the stories about people's career in Scala. This kind of stories are mind opening, and also tells Scala enthusiasts how to better plan their careers.

Thanks for reading my story. See you in the next part!

{{< tip >}}
Feel free to connect with me in [LinkedIn](https://www.linkedin.com/in/eason-du-03543279)
{{< /tip >}}
