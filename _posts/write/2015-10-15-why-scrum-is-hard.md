---
layout: post
title: "Why Scrum is hard"
modified:
categories: write
excerpt:
tags: [Development]
comments: true
image:
  feature:
date: 2015-10-19T08:08:50-04:00
---

![](http://ecx.images-amazon.com/images/I/51s2gkMEa1L._SX327_BO1,204,203,200_.jpg){: .center-image }

I must start by saying that while Scrum is hard, there may be no better way. My experience has been with the classical SDLC and Scrum, and I'd choose the latter every day of the week, and twice on Sundays.

But, when you read books like the one above it almost appears as if it's the easiest thing to do. It is not. Knowing the pitfalls is important because then you can watch out for them, and try to avoid them. I mention some of the pitfalls below, but give no suggestions on how to avoid them. It will vary from situation to situation, and in some cases there might be no easy solutions at all.

So let's start with the pitfalls you need to look out for.

## No multi-tasking

A key point of Scrum is that engineers estimate user stories and remain fully focused on them, during the sprint. 

Easier said than done. 

Most development teams work on products whose versions already exist in the market. And they are  the same engineers that need to respond to customer issues when the arise during the sprint. Typically, this is managed by allocating "x%" of bandwidth for customer escalations during the sprint...but that just looks good on spreadsheets and presentations. Soon as the first P1 case comes rushing in, all plans go up in smoke. And the sprint deliverables take a beating.

A possible solution is to have separate teams - one for main-line development, and another for handling customer escalations. That does not work well too, because that kind of separation is not healthy. The team handling customer escalations remains low on motivation, while the team working on main-line development remains disconnected from the real customer issues. Having two team itself may not be an option due to other constraints.

So, to be successful in this area, think how you will ensure that the Scrum team focuses *completely and completely* on the sprint stuff throughout the sprint and the release.

## "Scrum teams should have all the skills needed to do the job"..."And be no more than 3-9"

While the book mentions that the Scrum team needs to be able to discharge responsibilities of sales, production, design, distribution...I will limit this to development, and state that even _that_ is hard to achieve. If you're working on an enterprise level product it's quite possible that the overall effort will involve 30-40 or more team members, to just *develop the code*, leave alone distribution, build, sales, technical publications... 

The typical solution to this situation is to establish a "Scrum of Scrums". So, while each Scrum team is still 3-9 members, there maybe 5-10 Scrum teams that all need to work together to make sure the release happens. Now imagine how much more harder that is. 

Taken together, all Scrum teams will span 2 or 3 timezones at least. People who've never met face to face. People whose cultures are as different as chalk and cheese. With extremely different educational background. And to repeat - people who have never met face to face. 

How can such teams be "transcendent" in performance? That big word translates to something a friend of mine and me used to do in football as kids. I just knew where he would pass the ball and be there even before he had begun the kick. 

To make things harder, such Scrum of Scrums meetings often happen at un-earthly hours for some timezone or the other because the goal is to fit all Scrum masters in one on-line teleconferencing meeting. Happiness takes a nose dive if you have recurring weekly meetings at 12:45am in the night. And being happy is an important ingredient as has been mentioned several times in the book.

How can a SoS meetings be effective, and still maintain the spirit of Scrum...which is to be happy at work?

## "2 week sprints, which demonstrate value to customer at the end of it"

The only way you can develop code that has actual value to a user within 2 weeks is if all the code you write is fully unit tested and whose functionality can be tested via automation. There simply is no way to do manual testing *and* have two week sprints. 

In the world of enterprise software, if you are writing a product from scratch (very rare) or have inherited a product that has existing unit tests (rare) you are in indeed lucky. If you're like the rest of the world, the product you inherited was written in 1990s, had no unit  tests and was not even written in a way that _could_ make it possible to have unit tests - not without a large refactoring of the code base. 

While you _can_ write unit tests for the new code you, it's not always that straightforward. Often times, the new code will call into old legacy code which will not lend itself to easy mocking and stubbing routines. 

The other challenge is automation.

Creating automation tests at the start of the feature is a challenge. Often times, the UI is not frozen and so the automation engineers would rather wait for the flux to all "settle down" before diving into the automation. That's a little bit of waterfall right there. 

Do you have an awesome continuous integration pipeline where every checking triggers a unit test suite that covers close to 100% of the code path? 

Do you then have the CI pipeline automatically trigger a full automated testing all the features of the product to make sure no regressions were introduced?

## "Everyone can do everything"

On Page 80, of the book, the author very rightly points out a common problem with stand-ups...treating it as "I did this, I'll do that" and then on to the next person. I've been in many stand-ups that sounded exactly like this. Jeff, the author, suggests that the approach be one of "I'm having a problem with the defensive lineman" to which an offensive blocker (not sure why he is offensive, maybe bad breath?) might respond, "I'll take care of that, I'll open the line". 

That's quite nice, except it does not work in real world issues. More often than not, you have exactly one person who has the skills to handle the complex task relating to that active proxy component's interaction with the web server. And it's not so simple as "opening up the line". It may take months for someone else to know about that piece of code, well enough to make changes. 

The intense nature of code, and the pre-requisites around them, necessitate the growth of specialists in the team. This is sometimes unfortunate, as specialists can become [sacred cows]({% post_url /write/2015-10-10-no-sacred-cows%}) over time and cause other problems. But it is a fact that complex production level code cannot be simply be worked on by someone...just because someone else got blocked.

Do you have full redundancy in your team in terms of skill-sets? If you have good for you. If not, your stand-ups might be plain old status meetings under the hood.

## One meeting per day

This is another Scrum tenet: There should be only one meeting per day and that is the 15 minute daily stand up. This is almost never the case. 

There will be customer escalation meetings. Road-map meetings. Strategy meetings. Special demo meetings for visitors from another geography. Lunch meetings. Meetings with HR. Company all-hands. Meetings to reduce technical debt that was not part of the sprint. Meetings for various initiatives such as increasing innovation in the company, improving rewards and recognition, making code reviews more efficient. The list of meetings is endless.

How often do you have a "one meeting day" day?

## Final thoughts

These are just _some_ of the challenges of Scrum. There are more. 

Nevertheless, [Scrum - The Art of Doing Twice the Work in Half the Time](http://www.amazon.in/Scrum-Doing-Twice-Work-Half/dp/038534645X), is one of the best books on the topic. The [other really good one](http://www.amazon.in/Succeeding-Agile-Software-Development-Using-ebook/dp/B002TIOYWQ/ref=asap_bc?ie=UTF8) is by Mike Cohn. So by all means do Scrum. But don't for a minute assume that it is as easy as it will appear in most books and trainings. If that were the case, we would all be surrounded by amazing software ready even before we want it because everyone would be doing Scrum. That's simply not the case today.

I once asked a colleague, "How do you know if you are Agile or not?". She had a great answer. 

She said, "When your release is a non-event."

So are your releases non-events too? 
