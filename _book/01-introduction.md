---
output:
  pdf_document: default
  html_document: default
---
\mainmatter




# (PART) Foundations {-}


# Telling Stories with Data

**Required material**

- Read *Counting the Countless*, [@keyes2019].
- Watch *Data Science Ethics in 6 Minutes*, [@register2020].


## On telling stories

Like many parents, when our children were born, one of the first things that my wife and I did regularly was read stories to them. In doing so we carried on a tradition that has occurred for millennia. Myths, fables, and fairy tales can be seen and heard all around us. Not only are they entertaining but they enable us to learn something about the world. While *The Very Hungry Caterpillar* [@veryhungry] may seem quite far from the world of dealing with data, there are similarities. Both are trying to tell a story and teaching us something about the world.

When using data, we try to tell a convincing story. It may be as exciting as predicting elections, as banal as increasing internet advertising click rates, as serious as finding the cause of a disease, or as fun as forecasting basketball games. In any case the key elements are the same. The English author, E. M. Forster, described the aspects common to all novels as: story, people, plot, fantasy, prophecy, pattern, and rhythm [@forster]. Similarly, when we tell stories with data, there are common concerns, regardless of the setting:

1. What is the dataset? Who generated the dataset and why?
2. What is the process that underpins the dataset? Given that process, what is missing from the dataset or been poorly measured? Could other datasets have been generated, and if so, how different could they have been to the one that we have?
3. What is the dataset trying to say, and how can we let it say this? What else could it say? How do we decide between these?
4. What are we hoping others will see from this dataset, and how can we convince them of this? How much work must we do to convince them? To what extent can we share how we came to believe this?
5. Who is affected by the processes and outcomes related to this dataset? To what extent are they represented in the dataset, and have they been part of conducting the analysis?

In the past, certain elements of telling stories with data were easier. For instance, experimental design has a long and robust tradition within agricultural and medical sciences, physics, and chemistry. Student's t-distribution was identified in the early 1900s by a chemist, William Sealy Gosset, who was working at Guinness, a beer manufacturer, and needed to assess the quality of the beer [@boland1984biographical]! It would have been possible for him to randomly sample the beer and change one aspect at a time. 

Many of the fundamentals of the statistical methods that we use today were developed in such settings. There, it was typically possible to establish control groups and randomize; and in these settings there were fewer ethical concerns. A story told with the resulting data is likely to be fairly convincing.

Unfortunately, little of this applies these days, given the diversity of settings to which statistical methods are applied. On the other hand, we have many advantages. For instance, we have well-developed statistical techniques, easier access to large datasets, and open-source statistical languages such as R [@citeR]. But the difficulty of conducting traditional experiments means that we must also turn to other aspects to tell a convincing story.

## Workflow components

There are five core components to the workflow needed to tell stories with data:

1. **Plan** and sketch an endpoint.
2. **Simulate** some reasonable data and consider that.
3. **Acquire** and prepare the real data.
4. **Explore** and understand that dataset.
5. **Share** what we did and what we found.

We begin by **planning and sketching an endpoint** because this ensures that we think carefully about where we want to go. It forces us to deeply consider our situation, acts to keep us focused and efficient, and helps reduce scope creep. In *Alice's Adventures in Wonderland* [@citealice], Alice asks the Cheshire Cat which way she should go. The Cheshire Cat replies by asking where Alice would like to go. And when Alice replies that she does not mind, so long as she gets somewhere, the Cheshire Cat says then the direction does not matter because you will always get somewhere if you 'walk long enough'. The issue, in our case, is that we typically cannot afford to walk aimlessly for long. While it may be that the endpoint needs to change, it is important that this is a deliberate, reasoned, decision. And that is only possible given an initial target. There is no need to spend too much time on this to get a lot of value from it. Often five minutes with paper and pen, is enough.

The next step is to **simulate data** because that forces us into the details. It helps with cleaning and preparing the dataset because it focuses us on the classes in the dataset and the distribution of the values that we expect. For instance, if we were interested in the effect of age-groups on political preferences, then we may expect that our age-group column would be a factor, with four possible values: '18-29', '30-44', '45-59', '60+'. The process of simulation provides us with clear features that our real dataset should satisfy. We could use these features to define tests that would guide our data cleaning and preparation. For instance, we could check our real dataset for age-groups that are not one of those four values. When those tests pass, we could be confident that our age-group column only contains values that we expect.

Simulating data is also important when we turn to the statistical modelling stage. When we are at that stage, we are concerned with whether the model reflects what is in the dataset. The issue is that if we go straight to modelling the real dataset, then we do not know whether we have a problem with our model. We simulate data so that we precisely know the underlying data generation process. We then apply the model to that simulated dataset. When we get out what we put in, then we know that our model is performing appropriately, and can turn to the real dataset. Without that initial application to simulated data, it would be more difficult to have confidence in our model.

Simulation is often cheap---almost free given modern computing resources and statistical programming languages---and fast. It provides 'an intimate feeling for the situation' [@hamming1996, p. 239]. The way to proceed is to start with a simulation that just contains the essentials, get that working, and to then complicate it.

**Acquiring and preparing the data** that we are interested in is an often-overlooked stage of the workflow. This is surprising because it can be one of the most difficult stages and requires many decisions to be made. This is increasingly the subject of research. For instance, it has been found that decisions made during this stage greatly affect statistical results [@huntington2021influence]. 

At this stage of the workflow, it is common to feel a little overwhelmed. Typically, the data we can acquire leave us a little scared. There may be too little of it, in which case we worry about how we are going to be able to make our statistical machinery work. Alternatively, we may have the other problem and be worried about how we can even begin to deal with such a large amount of data.

> Perhaps all the dragons in our lives are princesses who are only waiting to see us act, just once, with beauty and courage. Perhaps everything that frightens us is, in its deepest essence, something helpless that wants our love.
>
> @rilke

Developing comfort in this stage of the workflow unlocks the rest of it. The dataset that is needed to tell a convincing story is in there, but we need to iteratively remove everything that is not the data that we need, and to then shape that which is.

After we have a dataset, we then want to **explore and understand ** certain relationships in that dataset. The use of statistical models to understand the implications of our data is not free of bias, nor are they 'truth'; they do what we tell them to do. Within a workflow to tell stories with data, statistical models are tools and approaches that we use to explore our dataset, in the same way that we may use graphs and tables. They are not something that will provide us with a definitive result but will enable us to understand the dataset more clearly in a particular way.

By the time we get to this step in the workflow, to a large extent, the model will reflect the decisions that were made in earlier stages, especially acquisition and cleaning, as much as it reflects any type of underlying process. Sophisticated modellers know that their statistical models are like the bit of the iceberg above the surface; they build on, and are only possible due to, the majority that is underneath, in this case, the data. But when an expert at the whole workflow uses modelling, they recognise that the results that are obtained are additionally due to choices about whose data matters, decisions about how to measure and record the data, and other aspects that reflect the world as it is, well before that data is available to their specific workflow.

Finally, we must **share** what we did and what we found, at as high a fidelity as is possible. Talking about knowledge that only you have, does not make you knowledgeable, and that includes knowledge that only 'past you' has. When communicating, we need to be clear about what decisions we made, why we made them, our findings, and the weaknesses of our approach. We are aiming to uncover something important (otherwise, why bother) so we write down everything, in the first instance, although this written communication may be supplemented with other forms of communication later. There are so many decisions that we must make in this workflow that we want to be sure that we are open about the entire thing---start to finish. This means much more than just the statistical modelling and creation of the graphs and tables, but everything. Without this, stories based on data do not have any credibility.

The world is not a rational meritocracy where everything is carefully and judiciously evaluated. Instead, we use shortcuts, hacks, and heuristics, based on our experience. Unclear communication will render even the best work moot, because it will not be thoroughly engaged with. While there is a minimum when it comes to communication, there is no upper limit to how impressive it can be. When it is the culmination of a thought-out workflow, at best, it obtains a certain *sprezzatura*, or studied carelessness. Achieving such mastery, is the work of years.



## Telling stories with data

A compelling story based on data can likely be told in around ten-to-twenty pages. Much less than this, and it is likely too light on some of the details. And while it is easy to write much more, often some reflection enables succinctness or for multiple stories to be separated. The best stories are typically based on research and independent learning.

It is possible to tell convincing stories even when it is not possible to conduct traditional experiments. These approaches do not rely on 'big data'---which is not a panacea [@meng2018statistical]---but instead on better using the data that are available. A blend of theory and application, combined with practical skills, a sophisticated workflow, and an appreciation for what one does not know, is often enough to create lasting knowledge.

The best stories based on data tend to be multi-disciplinary. They take from whatever field they need to, but almost always draw on: statistics, data visualisation, computer science, experimental design, economics, and information science (to name a few). As such, an end-to-end workflow requires a blend of skills from these areas. The best way to learn these skills is to use real-world data to conduct research projects where you:

- obtain and clean relevant datasets; 
- develop research questions; 
- use statistical techniques to explore those questions; and 
- communicate in a meaningful way. 

The key elements of telling convincing stories with data are:

1. Communication.
2. Ethics.
3. Reproducibility.
4. Questions.
5. Measurement.
6. Data collection.
7. Data cleaning.
8. Exploratory data analysis.
9. Modelling.
10. Scaling.

These elements are the foundation on which the workflow are built (Figure \@ref(fig:iceberg)).

\begin{figure}
\includegraphics[width=0.85\linewidth]{/Users/rohanalexander/Documents/book/figures/IMG_1820} \caption{The workflow builds on various elements}(\#fig:iceberg)
\end{figure}

This is a lot to master, but **communication** is the most important. Simple analysis, communicated well, is more valuable than complicated analysis communicated poorly. This is because the latter cannot be understood or trusted by others. A lack of clear communication sometimes reflects a failure by the researcher to understand what is going on, or even what they are doing. And so, while the level of the analysis should match the dataset, instruments, task, and skillset, when a trade-off is required between clarity and complication, it can be sensible to err on the side of clarity.

Clear communication means writing in plain language, with the help of tables, graphs, and technical terms, in a way that brings the audience along with you. It means setting out what was done and why, as well as what was found. The minimum hurdle is doing this in a way that enables another person to independently do what you did and find what you found. One challenge is that as you immerse yourself in the data, it can be difficult to remember what it was like when you first came to it. But that is where most of your audience will be coming from. Learning to provide an appropriate level of nuance and detail is especially difficult but is made easier by trying to write for the audience's benefit.

Active consideration of **ethics** is needed because the dataset likely concerns humans. This means considering things like: who is in the dataset, who is missing, and why? To what extent will our story perpetuate the past? And is this something that ought to happen? Even if the dataset does not concern humans, the story is likely being put together by humans, and we affect almost everything else. This means we have a moral responsibility to use data ethically, with concern for environmental impact, and inequity.

There are many definitions of ethics, but when it comes to telling stories with data, at a minimum it means considering the full context of the dataset [@datafeminism2020]. In jurisprudence, a textual approach to law means literally considering the words of the law as they are printed, while a purposive approach means laws are interpreted within a broader context. An ethical approach to telling stories with data means adopting the latter approach, and considering the social, cultural, historical, and political forces that shape our world, and hence our data [@crawford].

**Reproducibility** is required to create lasting knowledge about the world. It means that everything that was done---all of it, end-to-end---can be independently redone. Ideally, autonomous end-to-end reproducibility is possible; anyone can get the code, data, and environment, to verify everything that was done. Unfettered access to code is almost always possible. While that is the default for data also, it is not always reasonable. For instance, studies in psychology may have small, personally identifying, samples. One way forward is to openly share simulated data with similar properties, along with defining a process by which the real data could be accessed, given appropriate *bona fides*.

Curiosity provides internal motivation to explore a dataset, and associated process, to a proper extent. **Questions** tend to beget questions, and these usually improve and refine as the process of coming to understand a dataset carries on. In contrast to the stock Popperian approach to hypothesis testing often taught, questions are typically developed through a continuous and evolving process [@franklin2005exploratory]. It can be difficult to find an initial question. Selecting an area of interest can help, as can sketching a broad claim with the intent of evolving it into a specific question, and finally, bringing together two different areas. 

Developing a comfort and ease in the messiness of real-world data means getting to ask new questions each time the data update. And knowing a dataset in detail tends to surface unexpected groupings or values that you can then work with subject-area experts to understand. Becoming a bit of a 'mongrel' by developing a base of knowledge across a variety of areas is especially valuable, as is becoming comfortable with the possibility of initially asking dumb questions.

**Measurement** and **data collection** are about deciding how our world will become data. They are challenging. The world is so vibrant that it is difficult to reduce it to something that is possible to consistently measure and collect. Take, for instance, someone's height. We can, probably, all agree that we should take our shoes off before we measure height. But our height changes over the course of the day. And measuring someone's height with a tape measure will give different results to using a laser. If we are comparing heights between people or over time, it therefore becomes important to measure at the same time each day, using the same method. But that quickly becomes infeasible.

Most of the questions we are interested in will use data that are more complicated than height. How do we measure how sad someone is? How do we measure pain? Who decides what we will measure and how we will measure it? There is a certain arrogance required to think that we can reduce the world to a value and then compare these. Ultimately, we must, but it is difficult to consistently define what is to be measured. This process is not value-free. The only way to reasonably come to terms with this brutal reduction is to deeply understand, and respect what we are measuring and collecting. What is the central essence, and what can be stripped away?

Pablo Picasso, the twentieth century Spanish painter, has a series of drawings where he depicts the outline of an animal using only one line (Figure \@ref(fig:lumpthedog)). Despite their simplicity, we recognise which animal is being depicted---the drawing is sufficient to tell the animal is a dog, not a cat.  Could this be used to determine whether the dog is sick? Probably not. We would likely want a more detailed drawing. The decision as to which features should be measured and collected, and which to ignore, turns on context and purpose.

\begin{figure}

{\centering \includegraphics[width=0.85\linewidth]{/Users/rohanalexander/Documents/book/figures/lump} 

}

\caption{This drawing is clearly a dog, even though it is just one line}(\#fig:lumpthedog)
\end{figure}

**Data cleaning and preparation** is a critical part of using data. We need to massage the data available to us into a dataset that we can use. This requires making a lot of decisions. The data cleaning and preparation stage is critical, and worthy of as much attention and care as any other. 

Consider a survey that collected information about gender using four options: 'man', 'woman', 'prefer not to say', 'other', where 'other' dissolved into an open textbox. When we come to that dataset, we are likely to find that most responses are either 'man' or 'woman'. We need to decide what to do about 'prefer not to say'. If we drop it from our dataset, then we are actively ignoring these respondents. If we do not drop it, then it makes our analysis more complicated. Similarly, we need to decide how to deal with the open text responses. Again, we could drop these responses, but this ignores the experiences of some of our respondents. Another option is to merge this with 'prefer not to say', but that shows a disregard for our respondents, because they specifically did not choose that option. 

There is no easy, nor always-correct, choice in many data cleaning and preparation situations. It depends on context and purpose. Data cleaning and preparation involves making many choices like this, and so it is vital to record every step so that others can understand what was done and why. Data never speak for themselves; they are the dummies of the ventriloquists that cleaned and prepared them.

The process of coming to understand the look and feel of a dataset is termed **exploratory data analysis** (EDA). This is an open-ended process. We need to understand the shape of our dataset before we can formally model it. The process of EDA is an iterative one that involves producing summary statistics, graphs, tables, and sometimes even some modelling. It is a process that never formally finishes and requires a variety of skills. 

It is difficult to delineate where EDA ends and formal statistical modelling begins, especially when considering how beliefs and understanding develop [@Hullman2021Designing]. But at its core, 'EDA starts from the data', and involves immersing ourselves in it [@Cook2021Foundation]. EDA is not something that is typically explicitly part of our final story. But it has a central role in how we come to understand the story we are telling. And so, it is critical that all the steps taken during EDA are recorded and shared.

**Statistical modelling** has a long and robust history. Our knowledge of statistics has been built over hundreds of years. Statistics is not a series of dry theorems and proofs but is instead a way of exploring the world. It is analogous to 'a knowledge of foreign languages or of algebra: it may prove of use at any time under any circumstances' [@bowley, p. 4]. A statistical model is not a recipe to be blindly followed in an if-this-then-that way but is instead a way of understanding data [@islr]. Modelling is usually required to infer statistical patterns from data. More formally, 'statistical inference, or "learning" as it is called in computer science, is the process of using data to infer the distribution that generated the data' [@wasserman p. 87]. 

Statistical significance is not the same as scientific significance, and we are realising the cost of what has been the dominant paradigm. It is rarely appropriate to put our data through some arbitrary pass/fail statistical test. Instead, the proper use for statistical modelling is as a kind of echolocation. We listen to what comes back to us from the model, to help learn about the shape of the world, while recognising that it is only one representation of the world.

The use of statistical programming languages, such as R, enables us to rapidly **scale** our work. This refers to both inputs and outputs. It is basically just as easy to consider 10 observations as 1,000, or even 1,000,000. This enables us to more quickly see the extent to which our stories apply. It is also the case that our outputs can be consumed as easily by one person as by 10, or 100. Using an Application Programming Interface (API) it is even possible for our stories to be considered many thousands of times each second.






## How do our worlds become data?

> There is the famous story by Eddington about some people who went fishing in the sea with a net. Upon examining the size of the fish they had caught, they decided there was a minimum size to the fish in the sea! Their conclusion arose from the tool used and not from reality.
>
>  @hamming1996 [p. 177]

To a certain extent we are wasting our time. We have a perfect model of the world---it is the world! But it is too complicated. If we knew perfectly how everything was affected by the uncountable factors that influence it, then we could perfectly forecast a coin toss, a dice roll, and every other seemingly random process each time. But we cannot. Instead, we must simplify things to that which is plausibly measurable, and it is that which we define as data. Our data are a simplification of the messy, complex, world from which they were generated.

There are different approximations of 'plausibly measurable'. Hence, datasets are always the result of choices. We must decide whether they are nonetheless reasonable for the task at hand. We use statistical models to help us think deeply about, explore, and hopefully come to better understand, our data.

Much of statistics is focused on considering, thoroughly, the data that we have. And that was appropriate for when our data were predominately agricultural, astronomical, or from the physical sciences. But with the rise of data science, mostly because of the value of its application to datasets generated by humans, we must also actively consider what is not in our dataset. Who is systematically missing from our dataset? Whose data does not fit nicely into the approach that we are using and are hence is being inappropriately simplified? If the process of the world becoming data necessarily involves abstraction and simplification, then we need to be clear about the points at which we can reasonably simplify, and those which would be inappropriate, recognising that this will be application specific.

The process of our world becoming data necessarily involves measurement. Paradoxically, often those that do the measurement and are deeply immersed in the details have less trust in the data than those that are removed from it. Even seemingly clear tasks, such as measuring distance, defining boundaries, and counting populations, are surprisingly difficult in practice. Turning our world into data requires many decisions and imposes much error. Among many other considerations, we need to decide what will be measured, how accurately we will do this, and who will be doing the measurement. 

> **Oh, you think we have good data on that!** An important example of how something seemingly simple quickly becomes difficult is maternal mortality. That refers to the number of women who die while pregnant, or soon after a termination, from a cause related to the pregnancy or its management [@matmortality]. It is difficult but critical to turn the tragedy of such a death into cause-specific data because that helps mitigate future deaths. Some countries have well-developed civil registration and vital statistics (CRVS). These collect data about every death. But many countries do not have a CRVS and so not every death is recorded. Even if a death is recorded, defining a cause of death may be difficult, especially when there is a lack of qualified medical personal or equipment. Maternal mortality is especially difficult because there are typically many causes. Some CRVS have a checkbox on the form to specify whether the death should be counted as maternal mortality. But even some developed countries have only recently adopted this. For instance, it was only introduced in the US in 2003, and even in 2015 Alabama, California, and West Virginia had not adopted the standard question [@macdorman2018failure].

We typically use various instruments to turn the world into data. In astronomy, the development of better telescopes, and eventually satellites and probes, enabled new understanding of other worlds. Similarly, we have new instruments for turning our own world into data being developed each day. Where once a census was a generational-defining event, now we have regular surveys, transactions data available by the second, and almost all interactions on the internet become data of some kind. The development of such instruments has enabled exciting new stories.

Our world imperfectly becomes data. If we are to nonetheless use data to learn about the world, then we need to actively seek to understand the ways they are imperfect and the implications of those imperfections.


## What is data science and how should we use it to learn about the world

There is no agreed definition of data science, but a lot of people have tried. For instance, @r4ds say it is '...an exciting discipline that allows you to turn raw data into understanding, insight, and knowledge.' Similarly, @leekandpeng say it is '...the process of formulating a quantitative question that can be answered with data, collecting and cleaning the data, analyzing the data, and communicating the answer to the question to a relevant audience.' @moderndatascience say it is '...the science of extracting meaningful information from data'. @craiu2019hiring argues that the lack of certainty as to what data science is might not matter because '...who can really say what makes someone a poet or a scientist?' He goes on to broadly say that a data scientist is '...someone with a data driven research agenda, who adheres to or aspires to using a principled implementation of statistical methods and uses efficient computation skills.'

In any case, alongside specific, technical, definitions, there is value in having a simple definition, even if we lose a bit of specificity. Probability is often informally defined as 'counting things' [@citemcelreath, p. 10]. In a similar informal sense, data science can be defined as something like: humans measuring stuff, typically related to other humans, and using sophisticated averaging to explain and predict.

That may sound a touch cute, but Francis Edgeworth, the nineteenth century statistician and economist, considered statistics to be the science 'of those Means which are presented by social phenomena', so it is in good company [@edgeworth1885methods]. In any case, one feature of this definition is that it does not treat data as *terra nullius*, or nobody's land. Statisticians tend to see data as the result of some process that we can never know, but that we try to use data to come to understand. Many statisticians care deeply about data and measurement, but there are many cases in statistics where data kind of just appear; they belong to no one. But that is never actually the case.

Data is generated, and then must be gathered, cleaned, and prepared, and these decisions matter. Every dataset is *sui generis*, or a class by itself, and so when you come to know one dataset well, you just know one dataset, not all datasets.

Much of data science focuses on the 'science', but it is important to also focus on 'data'. And that is another feature of that cutesy definition of data science. A lot of data scientists are generalists, who are interested in a broad range of problems. Often, the thing that unites these is the need to gather, clean, and prepare messy data. And often it is the specifics of those data that requires the most time, that updates most often, and that are worthy of our most full attention.

@Jordan2019Artificial describes being in a medical office and being given some probability, based on prenatal screening, that his child, then a fetus, had Down syndrome. By way of background, one can test to know for sure, but that test comes with the risk of the fetus not surviving, so this initial screening probability matters. @Jordan2019Artificial found those probabilities were being determined based on a study done a decade earlier in the UK. The issue was that in the ensuing 10 years, imaging technology had improved so the test was not expecting such high-resolution images and there had been a subsequent (false) increase in Down syndrome diagnoses when the images improved. There was no problem with the science, it was the data.

It is not just the 'science' bit that is hard, it is the 'data' bit as well. For instance, researchers went back and examined one of the most popular text datasets in computer science, and they found that around 30 per cent of the data were inappropriately duplicated [@bandy2021addressing]. There is an entire field---linguistics---that specialises in these types of datasets, and inappropriate use of data is one of the dangers of any one field being hegemonic. The strength of data science is that it brings together folks with a variety of backgrounds and training to the task of learning about some dataset. It is not constrained by what was done in the past. But this means that we must go out of our way to show respect for those who do not come from our own tradition, but who are nonetheless as similarly interested in a dataset as we are. Data science is multi-disciplinary and increasingly critical; hence it must reflect our world. There is a pressing need a diversity of backgrounds, of approaches, and of disciplines in data science. 

Our world is messy, and so are our data. To successfully tell stories with data you need to become comfortable with the fact that the process will be difficult. Hannah Fry, the British mathematician, describes spending six months rewriting code before it solved her problem [@hannahfryft]. You need to learn to stick with it. You also need to countenance failure, and you do this by developing resilience and having intrinsic motivation. The world of data is about considering possibilities and probabilities, and learning to make trade-offs between them. There is almost never anything that we know for certain, and there is no perfect analysis.

Ultimately, we are all just telling stories with data, but these stories are increasingly among the most important in the world.






## Exercises and tutorial

### Exercises

1. According to @register2020 data decisions affect (pick one)? 
    a. Real people. 
    b. No one. 
    c. Those in the training set. 
    d. Those in the test set.
2. In your own words, what is data science?
3. According to @keyes2019 what is perhaps a more accurate definition of data science (pick one)? 
    a. The inhumane reduction of humanity down to what can be counted.
    b. The quantitative analysis of large amounts of data for the purpose of decision-making.
    c. Data science is an inter-disciplinary field that uses scientific methods, processes, algorithms, and systems to extract knowledge and insights from many structural and unstructured data.
4. Imagine that you have a job in which including 'race' as an explanatory variable improves the performance of your model. What types of issues would you consider when deciding whether to include this variable in production? What if the variable was sexuality?
5. Re-order the following steps of the workflow to be correct:
    1. Simulate.
    2. Acquire.
    3. Share.
    4. Plan.
    5. Explore.
6. According to @crawford, which of the following forces shape our world, and hence our data (select all that apply)? 
    a. Political.
    b. Historical.
    c. Cultural.
    d. Social.
7. What is required to tell convincing stories (select all that apply)? 
    a. Sophisticated workflow.
    b. Practical skills.
    c. Big data.
    d. Humility about one's own knowledge.
    e. Theory and application.
8. Why is ethics a key element of telling convincing stories?
    
    
### Tutorial

The purpose of this tutorial is to clarify in your mind the difficulty of measurement, even of seemingly simple things, and hence the likelihood of measurement issues in more complicated areas. 

1. Please obtain some seeds for a fast-growing plant such as radishes, mustard greens, or arugula. Plant the seeds and measure how much soil you used. Water them and measure the water you used. Each day take a note of any changes. More generally, measure and record as much as you can. Note your thoughts about the difficulty of measurement. Eventually your seeds will sprout, and you should measure how big they are. We will return to use the data that you put together.
2. While you are waiting for the seeds to sprout, and for one week only, please measure the length of your hair daily. Write a one-or-two-page paper about what you found and what you learned about the difficulty of measurement.






