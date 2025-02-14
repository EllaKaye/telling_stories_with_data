
# Concluding remarks {#concludingremarks}

**Required material**

- Watch *Wrong Again! 30+ Years of Statistical Mistakes*, [@gelmansmistakes].

## Concluding remarks

There is an old saying, something along the lines of 'may you live in interesting times'. Possibly every generation feels this way, but we sure live in interesting times. In this book, we have covered a broad range of essential skills that would allow you to tell stories with data. But we are just getting started.

In a little over a decade data science has gone from something that barely existed, to a defining part of academia and industry. The extent and pace of this change has many implications for those learning data science. For instance, it may imply that one should not just make decisions that optimize for what data science looks like right now, but also what could happen. While that is a little difficult, that is also one of the things that makes data science so exciting. That might mean choices like:

- taking courses on fundamentals, not just fashionable applications;
- reading books, not just whatever is trending; and
- trying to be at the intersection of at least a few different areas, rather than hyper-specialized.

One of the most exciting times when you learn data science is realizing that you just love playing with data. A decade ago, this did not fit into any particular department, these days it fits into almost any of them. Data science needs diversity, both in terms of approaches and applications. It is increasingly the most important work in the world and hegemonic approaches have no place. It is just such an exciting time to be enthusiastic about data and able to build.


## Some issues

Data science draws from a variety of disciplines. But there are a variety of concerns that are common across them. Here we detail a few.

**1. How do we write unit tests for data science?**

<!-- **UPDATE to add in functional tests and stuff** -->

One thing that computer scientists know is the importance of unit tests. Basically this just means writing down the small checks that we do in our heads all the time. Like if we have a column that purports to the year, then it's unlikely that it's a character, and it's unlikely that it's an integer larger than 2500, and it's unlikely that it's a negative integer. We know all this, but writing unit tests has us write this all down.

In this case it's obvious what the unit test looks like. But more generally, we often have little idea what our results should look like if they're running well. The approach that I have taken is to add simulation—so we simulate reasonable results, write unit tests based on that, and then bring the real data to bear and adjust as necessary. But I really think that we need extensive work in this area because the current state-of-the-art is lacking.

**2. What happened to the machine learning revolution?**

I don't understand what happened to the promised machine learning revolution in social sciences. Specifically, I am yet to see any convincing application of machine learning methods that are designed for prediction to a social sciences problem where what we care about is understanding. I would like to either see evidence of them or a definitive thesis about why this can't happen. The current situation is untenable where folks, especially those in fields that have been historically female, are made to feel inferior even though their results are no worse.

**3. What do we do about p-values and power?**

As someone who learnt statistics from economists, but now is partly in a statistics department, I do think that everyone should learn statistics from statisticians. This isn't anything against economists, but the conversations that I have in the statistics department about what statistical methods are and how they should be used are very different to those that I have had in other departments.

I think the problem is that people outside statistics, treat statistics as a recipe in which they follow various steps and then out comes a cake. With regard to ‘power'—it turns out that there were a bunch of instructions that no one bothered to check—they turned the oven on to some temperature without checking that it was 180C, and that's fine because whatever mess came out was accepted because the people evaluating the cake didn't know that they needed to check the temperature had been appropriately set. (I am ditching this analogy right now).

As you know, the issue with power is related to the broader discussion about p-values, which basically no one is taught properly, because it would require changing an awful lot about how we teach statistics i.e. moving away from the recipe approach.

And so, my specific issue is that people think that statistics is a recipe to be followed. They think that because that's how they are trained especially in social sciences like political science and economics, and that's what is rewarded. But that's not what these methods are. Instead, statistics is a collection of different instruments that let us look at our data in a certain way. I think that we need a revolution here, not a metaphorical tucking in of one's shirt.


**4. How do we teach data science?**

We are beginning to start to have agreement on what the foundations of data science are. It involves computational thinking, concern for sampling, statistics, graphics, Git/GitHub, SQL, command line, comfort with messy data, comfort across a few languages including R and Python. But we have very little agreement on how best to teach it. Partly this is because data science instructors often come different fields, but also it is also partly a difference in resources and priorities.



**5. What is happening at the data cleaning and preparation stage?**

We basically do not have a good understanding how much any of this matters. @huntington2021influence showed that hidden research decisions have a big effect on subsequent estimates, sometimes greater than the standard errors. Such findings invalidate claims. We need much more investigation of how these early stages of the data science workflow affect the conclusions.



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

We often hear the phrase let the data speak. Hopefully by this point you understand that never happens. All that we can do is to acknowledge that we are the ones using data to tell stories, and strive and seek to make them worthy.

> It was her voice that made  
> The sky acutest at its vanishing.  
> She measured to the hour its solitude.  
> She was the single artificer of the world  
> In which she sang. And when she sang, the sea,  
> Whatever self it had, became the self  
> That was her song, for she was the maker.
> 
> 'The Idea of Order at Key West', [@wallacestevens]
