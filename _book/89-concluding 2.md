
# Concluding remarks {#concludingremarks}

**STATUS: Under construction.**


**Required material**

- Watch *Wrong Again! 30+ Years of Statistical Mistakes*, [@gelmansmistakes].


## Concluding remarks

There is an old saying, something along the lines of 'may you live in interesting times'. I am not sure if every generation feels this, but we sure live in interesting times. In this book, I have tried to convey some essentials that I think would allow you to contribute. But we are just getting started.

I am 35 and so I am in the 'data science didn't exist when I was an undergraduate' generation. In a little over a decade data science has gone from something that barely existed to a defining part of academia and industry. What does that imply for for you? It may imply that one should not just be making decisions that optimize for what data science looks like right now, but also what could happen. While that's a little difficult, that’s also one of the things that makes data science so exciting. That might mean choices like:

- taking courses on fundamentals, not just fashionable applications;
- reading books, not just whatever is trending; and
- trying to be at the intersection of at least a few different areas, rather than hyper-specialized.

I am just someone who likes to play with data using R. A decade ago I wouldn't have fit into any particular department. I am lucky that these days there is space in data science for someone like me.  And the nice thing about what we now call data science is that there's space for you as well.

Data science needs diversity. Data science needs your intelligence and enthusiasm. It needs you to be in the room, and able to make contributions. We live in interesting times and it's just such an exciting time to be enthusiastic about data. I can't wait to see what you build.


## Some issues

1. How do we write unit tests for data science?

**UPDATE to add in functional tests and stuff**

One thing that working with real computer scientists has taught me is the importance of unit tests. Basically this just means writing down the small checks that we do in our heads all the time. Like if we have a column that purports to the year, then it's unlikely that it's a character, and it's unlikely that it's an integer larger than 2500, and it's unlikely that it's a negative integer. We know all this, but writing unit tests has us write this all down.

In this case it's obvious what the unit test looks like. But more generally, we often have little idea what our results should look like if they're running well. The approach that I have taken is to add simulation—so we simulate reasonable results, write unit tests based on that, and then bring the real data to bear and adjust as necessary. But I really think that we need extensive work in this area because the current state-of-the-art is lacking.

2. What happened to the machine learning revolution?

I don't understand what happened to the promised machine learning revolution in social sciences. Specifically, I am yet to see any convincing application of machine learning methods that are designed for prediction to a social sciences problem where what we care about is understanding. I would like to either see evidence of them or a definitive thesis about why this can't happen. The current situation is untenable where folks, especially those in fields that have been historically female, are made to feel inferior even though their results are no worse.

3. How do we think about power?

As someone who learnt statistics from economists, but now is partly in a statistics department, I do think that everyone should learn statistics from statisticians. This isn't anything against economists, but the conversations that I have in the statistics department about what statistical methods are and how they should be used are very different to those that I have had in other departments.

I think the problem is that people outside statistics, treat statistics as a recipe in which they follow various steps and then out comes a cake. With regard to ‘power'—it turns out that there were a bunch of instructions that no one bothered to check—they turned the oven on to some temperature without checking that it was 180C, and that's fine because whatever mess came out was accepted because the people evaluating the cake didn't know that they needed to check the temperature had been appropriately set. (I am ditching this analogy right now).

As you know, the issue with power is related to the broader discussion about p-values, which basically no one is taught properly, because it would require changing an awful lot about how we teach statistics i.e. moving away from the recipe approach.

And so, my specific issue is that people think that statistics is a recipe to be followed. They think that because that's how they are trained especially in social sciences like political science and economics, and that's what is rewarded. But that's not what these methods are. Instead, statistics is a collection of different instruments that let us look at our data in a certain way. I think that we need a revolution here, not a metaphorical tucking in of one's shirt.


4. How do we teach this stuff?



## Next steps

This book has covered much ground, and while we are toward the end of it, as the butler Stevens is told in the novel *The Remains of the Day* [@ishiguro]:

> The evening's the best part of the day. You've done your day's work. Now you can put your feet up and enjoy it.

Chances are there are aspects that you want to explore further, building on the foundation that you have established. If so, then I have accomplished what I set out to do. 

If you were new to data science at the start of this book, then the next step would be to backfill that which I skipped over, and I would recommend @timbersandfriends. After that, you should learn more about R in terms of data science by going through @r4ds. To deepen your understanding of R itself, go next to @advancedr.

If you are interested in learning more about causality then start with @Cunningham2021 and @theeffect.

If you are interested to learn more about statistics then begin with @citemcelreath, and then backfill with @bayesrules and solidify the foundation with @bda. You should probably also backfill some of the fundamentals around probability, starting with @wasserman.

There is only one next natural step if you are interested in learning more about statistical (what has come to be called machine) learning and that's @islr followed by @esl.

If you are interested in sampling then the next book to turn to is @lohr. To deepen your understanding of surveys and experiments, go next to @fieldexperiments in combination with @kohavi.

For developing better data visualization skills, begin by turning to @healyviz, but then after that, develop strong foundations, such as @grammarofgraphics. For writing, it would be best to turn inward. Force yourself to write and publish everyday for a month. Then do it again and again. You will get better. That said, there are some useful books, including @caroonworking and @stephenking.

<!-- Thinking through production and SQL and things like, a next natural step is... -->

We often hear the phrase let the data speak. Hopefully by this point you understand that never happens. All that we can do is to acknowledge that we are the ones using data to tell stories, and strive and seek to make them worthy.




## Exercises and tutorial


### Exercises


### Tutorial

### Paper

At about this point, the Final Paper (Appendix \@ref(final-paper)) would be appropriate.


