---
title: Processing Monsters Meets Career Day
date: '2012-11-22 17:53:42 -0500'
date_gmt: '2012-11-22 22:53:42 -0500'
categories:
- Scratch
- Processing
- Generative Art
tags: []
comments: []
---
It was almost exactly four years ago, back in December of 2008, that I was invited to give a brief talk to the Career Club at my son's elementary school about the profession of Software Engineering. At the time I had been reading Daniel Shiffman's book [Learning Processing](http://learningprocessing.com/ "Learning Processing"){:target="_blank"} and was thinking about how the Processing programming language could be used as a tool for introducing kids to programming.

The Career Club was organized by one of the teachers at the elementary school and consisted of kids in the fifth and sixth grades who were interested enough in learning about career paths that they were willing to give up their recess to hear folks like me blather on about what they did for a living. I felt it would be safe to come in as a presenter since my son, at the time, was in Kindergarten so I was in no danger of humiliating him with my presence at his school.

### On Being a Software Engineer

The obligatory first part of my presentation dealt with standard questions about my career choice.

**What is Software Engineering?**

I apologize, but I fell back on Wikipedia here, "software engineering is the application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software." What does that mean exactly? Software engineers don't just write code all willy-nilly, they employ a process so they can ensure that what they develop meets their customer's needs and is of the highest possible quality. A simplification I know...but that's the general idea, no?

**What is a typical day like?**

Oddly enough, my days mainly consist of supporting existing systems: making updates as required, tracking down and fixing bugs that may raise their ugly little heads, adding new features that our customers ask for. On occasion I'll have the opportunity to work on developing an entirely new application. This is where the full software engineering process comes into play, with requirements gathering, analysis and design, implementation, testing, and deployment.

**How did I become interested in Software Engineering?**

The earliest experience that was related to my future career was writing programs in APL (yes, that [APL](https://en.wikipedia.org/wiki/APL_(programming_language)APL "APL"){:target="_blank"}) at a summer camp at a local university. I don't remember exactly when this was, though it was probably in middle school. Despite being simplistic programs (e.g. calculate the area of a circle, convert temperature from Fahrenheit to Celsius) I thought this was very cool. Probably the most appealing thing about it was that I could control what the computer did by writing a short program. At about the same time my parents had bought an Apple II computer which I used to tap out programs in the BASIC programming language. Nothing earth shattering here, mainly simple games. I did write a program for keeping track of the money that my paper route customers owed me, though.

**How do you become a Software Engineer?**

The path I recommended was to pursue an undergraduate degree in Computer Science followed by graduate work in Software Engineering. This is, essentially, the route I had followed, though it was a bit more complicated along the way for me. If you're fortunate enough you may get to work for a company that will cover your graduate degree education expenses as mine had.

### Introducing Processing and Scratch

This was only a twenty minute presentation, mind you, and I wanted to give the kids something more than a dry talk about Software Engineering so I switched gears at this point to do a demo of two of the most accessible programming languages out there at the time, [Processing](https://www.processing.org/ "Processing"){:target="_blank"} and [Scratch](https://scratch.mit.edu/ "Scratch"){:target="_blank"}.

Processing was developed by [Casey Reas](http://reas.com/ "Casey Reas"){:target="_blank"} and [Ben Fry](https://benfry.com/ "Ben Fry"){:target="_blank"} back in 2001 at the MIT Media Lab when they were both students of [John Maeda](https://maedastudio.com/ "John Maeda"){:target="_blank"}. It is based on Java  and is intended primarily for use as a tool in the visual arts. For this reason it has been streamlined for drawing to the screen. A program written in Processing relies primarily on implementing two functions: setup and draw. A simple program that draws a circle 50 pixels in diameter centered in a 200x200 pixel display window is written as:

{% highlight java %}
void setup() {
  size(200, 200);
}
void draw() {
  ellipse(100, 100, 50, 50);
}
{% endhighlight %}

Which results in:

![Circle](/images/posts/2012/11/circle.png "Circle")

This is why I thought Processing would be a great way to introduce programming to kids. You can write a minimal amount of code and get immediate and gratifying results.

### Processing Monsters

Also about this time I had come across a website created by [Lukas Vojir](http://lukasvojir.com/ "Lukas Vojir"){:target="_blank"} called Processing Monsters. He had created this website as part of his effort to learn Processing and he encouraged others to submit their creations to post on his website. The only rules were that the monsters must be in black and white and may respond to mouse input only. His stated goal was to create a short music reactive video using the monsters.

The website as it looked in December of 2008:

![Processing Monsters](/images/posts/2012/11/ProcessingMonsters-580x542.png "Processing Monsters")

Among the creations on this website was one called Blink Eye Monster by [Lam Chi Fai](https://about.me/mb09 "Lam Chi Fai"){:target="_blank"}, aka mb09, which I found to be exceptionally well written. This sketch featured a snake-like creature that followed the path of the mouse pointer. The creature seemed to float above a field of grass that swayed gently whenever it passed.

![Blink Eye Monster](/images/posts/2012/11/BlinkEyeMonsterBW-580x290.png "Blink Eye Monster")

I took this sketch as an example of how a software problem can be broken down into parts. I asked the students to think about how the body of the monster was created.

I explained that as a Software Engineer one would analyze this problem and break it down into its constituent parts. The monster, for instance, is composed of an eye and body parts. We would likely express this in a class diagram similar to the one shown below:

![Blink Eye Monster Class Diagram](/images/posts/2012/11/Blink-Eye-Monster-Class-Diagram-580x259.png "Blink Eye Monster Class Diagram")

It turns out that the body is composed of a series of circles, diminishing in size from head to tail. By gradually diminishing the size and offsetting each circle it gives the illusion of a continuous form.

![Monster Body Parts](/images/posts/2012/11/MonsterBodyParts-580x290.png "Monster Body Parts")

The code to accomplish this is a bit complex, and involves quite a bit of trigonometry. I briefly showed the code for updating the position of a segment of the monster's body, but I didn't go into a detailed explanation as to how all this works.

{% highlight java %}
void Update(float _x, float _y)
{
  if(dist(x,y,_x,_y)> 5)
  {
    float d = dist(x,y,_x,_y);
    float angle = atan2((y-_y),(x-_x));
    x = _x + cos(angle) * 5;
    y = _y + sin(angle) * 5;
  }
  else
  {
    float d = dist(x,y,_x,_y);
    float angle = atan2((y-_y),(x-_x));
    x = _x + cos(angle) * d;
    y = _y + sin(angle) * d;
  }
}
{% endhighlight %}

The grass is constructed in a similar manner. Each blade of grass is composed of quadrilaterals of diminishing width aligned end to end. To illustrate this, in the image below I've eliminated the fill color and made the stroke visible. I've also reduced the number of grass blades and exaggerated their size by increasing the width factor.

![Grass Blades](/images/posts/2012/11/GrassBlades-580x290.png "Grass Blades")

Not only does the grass bend and sway based upon the motion of the monster, but Perlin noise is also employed to simulate gentle swaying due to wind. I don't know about you, but I was thoroughly impressed by the effort that Lam Chi Fai put into creating this sketch.
As you can tell, there is a lot going on in this one program that could be the basis of mathematics assignments in middle school on up.

### Scratch

Following my discussion of the Blink Eye Monster, I briefly demonstrated the Scratch programming environment and showed the students a couple of the games that are provided as examples with the tool. I also demonstrated how to create a basic program in Scratch by dragging and connecting programming blocks to build scripts.

![Scratch](/images/posts/2012/11/Screen-Shot-2012-11-22-at-5.46.56-PM-580x444.png "Scratch")

The Scratch website is also a great resource for sharing and learning about how to program. It's very easy to upload any program you've created, as well as to download and experiment with code that others have written.

### And Now for Something Completely Different...

In retrospect, I may have presented this differently. My goal was to get the kids in the audience excited about the idea of programming and envision themselves pursuing Software Engineering as a career. To that end, I think it may have been better to have involved them in the process, rather than having them listen to me while I demonstrated something on a screen.

So what would I have done instead? I think I would have involved them in a programming game, one that doesn't require the use of a computer. The objective of the game is to write a program that allows a robot to navigate from one end of the classroom to the other, avoiding any obstacles in its path. The obstacles could be desks or chairs scattered throughout the room. Likewise, the goal could be a desk, chair or a square laid out with masking tape on the floor. The only commands that the robot understands are turn left (90 degrees to left), turn right (90 degrees to right), or move n steps, where n is the number of steps forward that the robot should move. Each step could represent a tile in the floor, or if you're exceptionally ambitious, a grid could be laid out with masking tape in advance of the presentation.

The students would get a chance to study the obstacle course and then write down their program on paper. I would then ask for volunteers for a programmer and someone to play the part of the robot. The programmer would then read each step of their program aloud and the student playing the robot would follow their instructions. If the robot was able to successfully navigate to the goal, the obstacles would be rearranged and someone else would get the opportunity to be the programmer. Hopefully, several students would have had an opportunity to play the role of the programmer or robot within the allotted time.

At the end of the presentation, I would have then pointed the students to the Scratch and Processing websites and encouraged them to try their hand at writing a program using these tools.

### Final Thoughts

Some time later I received a card from the school, thanking me for presenting to the Career Club. Notice anything familiar?

![Career Day Thank You Note](/images/posts/2012/11/IMG_1324-580x753.jpg "Career Day Thank You Note")

Rather than the black and white field of grass as in the original program, the card shows the monster hovering over a field of green. Whoever drew the illustration for the card recalled that during the presentation I had briefly uncommented one of the original lines of code that had changed the fill color for each blade of grass from black to a random shade of green:

{% highlight java %}
col = color(51+random(5),200+random(55),90+random(165));
//col = color(0);
{% endhighlight %}

![Blink Eye Monster](/images/posts/2012/11/BlinkEyeMonster-580x290.png "Blink Eye Monster")

I don't know if anyone was inspired to pursue a career as a Software Engineer as a result of my presentation. Hopefully no one was deterred by it.

Unfortunately, I haven't had the opportunity to be involved in any Career Club presentations following this one. The following year the fifth and sixth grades for all elementary schools in the district were consolidated into a single school, my son's school is now Kindergarten to Fourth grade. I'm not sure if the Career Club was reconstituted at the new school. It would be a shame if it wasn't since I believe that this is the time in life when children start to form ideas about what they'll do as adults.

Sadly, the [Processing Monsters](http://www.rmx.cz/monsters/ "Processing Monsters"){:target="_blank"} website appears to be defunct as well. I'm not sure if a video was ever created using the various monsters that were submitted.

Fortunately there are still websites that allow you to share your Processing sketches with the world, among these are [OpenProcessing](https://www.openprocessing.org/ "OpenProcessing"){:target="_blank"} and [HasCanvas](https://experiments.withgoogle.com/hascanvas "HasCanvas"){:target="_blank"}.

![OpenProcessing](/images/posts/2012/11/OpenProcessing.png "OpenProcessing")

![HasCanvas](/images/posts/2012/11/HasCanvas-580x309.png "HasCanvas")

There is also a very neat project created by [Andreas Gysin](https://ertdfgcvb.xyz/ "Andreas Gysin"){:target="_blank"} called [The Abyss](https://www.creativeapplications.net/processing/the-abyss-tutorial/ "The Abyss"){:target="_blank"} which enables you to create your own creature and set it loose to roam about on the screen.

<iframe src="http://player.vimeo.com/video/24134931?color=ffffff" frameborder="0" width="740" height="400"></iframe>

My original inspiration for this post derives from the fact that Daniel Shiffman is out with a new book called "[The Nature of Code](https://natureofcode.com/ "The Nature of Code"){:target="_blank"}" where he explores mathematical models of natural systems using the Processing programming language. Like his previous book "Learning Processing" this is a very approachable book for learning programming and the mathematics behind simulation. I highly recommend it.

I would also like to extend my thanks to Lukas Vojir and Lam Chi Fai for their excellent work related to Processing. Their projects are what makes the internet such an amazing resource.

Finally, how would you present Software Engineering to fifth and sixth graders? What are your thoughts on using Scratch and Processing to introduce kids to programming? Do you think kids would get anything out of the programming game exercise I described? Let me know in the comments.
