---
Author: Henry
topic: Journey
---

The journey of finding a solution for memory management for my brother.

It is hard to manage all you need to learn systematically. People are easy to forget, and tend to stay away from what we are not good at. This is natural. My brother need to prepare for the College Entrance Examination, an exam with fixed range of materials. We analysed his mocking result this time and found three major parts that lead him lose points.

- do not know the knowledge
- being careless
- not familiar and run out of time

He estimated that each catagory takes about one third of the points that he lost. What they are doing at school is continue going over all the material, without focusing on the part that they don't understand or make more mistaktes. This is actually not an efficient way of learning. There is an easier solution that is tailored for each student, we need some tools to manage our memory.

For example. You might found one problem hard for you, generally, you either leave it there or understand it and then leave it there. Without a memory management system, you are not likely to come back to the problem. It is the same as learning something new, you may get it in a short time, and never come back.

[The forgetting curve](https://en.wikipedia.org/wiki/Forgetting_curve) revealed partly how memory works. And we can bring the knowledge back time and time again to help us memorize it. The question becomes, can we do that?

I came up with the idea that I am going to write an APP for it, and write the following specifications.
```
> Would building a database for learning make learning easier?
> How to integrate forget curve into general learning?
> Is there a related product?

Goal of the app: Help students improve their performance at exams by providing tracking tools for their unknown, unfamiliar and easy to forget knowledge.

Function:
- A database that covers knowledge and practice problems. or a tool to log problems (photo) and adding labels
- track the learning and practicing.
- using the forgetting curve to remind you of doing a review.

Implementation:
- An Android App that can run on pad and phone.[check]
- Take pictures and store it. [check]
- Label pictures. [check]
- tracking of review. [check]
- review reminder based on label and forgetting curve. [check]
- review and adjust label. [check]
- statistical analysis tools. [check]
```
Doesn't seem too hard, right?
But wait, is there an existing APP for that?
I searched on [Zhuhu](https://www.zhihu.com/answer/14429289) and the answer, thought not easy to found, is yes!

__Ankidroid!__

How can I forget this! I tried in university using it for vocabulary and even some other subjects. Anki allows you to create decks, which are collections of cards. For each car, you can put some problem in one side and answer on the other side. When you do the review, you can choose how you feel about the card, easy or hard. If you choose hard, it will show up soon. And if you choose easy, it will show up a few days later. Anki will help you manage the review time using the forgetting curve. It is cool and simple. I checked that It can actually upload photos and audios. Perfect!

Solution:
- use Ankidroid to record the problem and review timely
- use android pad or alternative, use epad. and with a cellphone.

But in Zhuhai No.1 Middle School, students are not allowed to use cellphone or tablets. Emmm...

But can I lock it to using Ankidroid only?
adding requirements: administrative level, lock the phone for other apps.

I found the answer is __Yes__!

- MIUI7 support this with kid mod, not available in later version
- APPlock is good, tried that.


**So the final solution would be:**

- getting an **android pad or phone** (pad has larger screen)
- install **Ankidroid** and **AppLock**
- create **decks** for **each subject** (deck for math)
- take **photos** of the problems that you feel **hard** and **label** them. (label: geometry)
- continue and **review timely**.
- an alternative of pad would be Epad, with E-ink creen, hand writing and Android support, but without camera. I feel like that would definitely be better for your eyes, but just take much more time to write down your problems.

Final words, I feel like I should use this method to study...
