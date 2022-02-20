--- 
title: "Telling Stories With Data"
author: "Rohan Alexander"
date: "19 February, 2022"
documentclass: krantz
bibliography: bibliography.bib
biblio-style: apalike
link-citations: yes
colorlinks: yes
lot: yes
lof: yes
site: bookdown::bookdown_site
monofont: "inconsolata"
description: "This book is about learning how to tell stories with data."
github-repo: RohanAlexander/telling_stories_with_data
graphics: yes
always_allow_html: true
cover-image: tellingstorieswithdatapainting.png
---




# Preface {-}

<div class="figure" style="text-align: center">
<img src="/Users/rohanalexander/Documents/book/figures/tellingstorieswithdatapainting.png" alt="Telling stories with data" width="90%" />
<p class="caption">(\#fig:unnamed-chunk-1)Telling stories with data</p>
</div>

This book will help you tell stories with data. It establishes a foundation on which you can build and share knowledge about an aspect of the world of interest to you based on data that you observe. Telling stories in small groups around a fire played a critical role in the development of humans and society [@wiessner2014embers]. Today our stories, based on data, can influence millions.

In this book we will explore, prod, push, manipulate, knead, and ultimately, try to understand the implications of data. A variety of features drive the choices in this book. 

The motto of the university from which I took my PhD is *naturam primum cognoscere rerum* or roughly 'learn the first nature of things'. But the original quote continues *temporis aeterni quoniam*, or roughly 'for eternal time'. We will do both of these things. I focus on tools, approaches, and workflows that enable you to establish lasting and reproducible knowledge.

When I talk of data in this book, it will typically be related to humans. Humans will be at the centre of most of our stories, and we will tell social, cultural, and economic stories. In particular, throughout this book I will draw attention to inequity both in social phenomena and in data. Most data analysis reflects the world as it is. Many of the least well-off face a double burden in this regard: not only are they disadvantaged, but the extent is more difficult to measure. Respecting those whose data are in our dataset is a primary concern, and so is thinking of those who are systematically not in our dataset. 

While data are often specific to various contexts and disciplines, the approaches used to understand them tend to be similar. Data are also increasingly global with resources and opportunities available from a variety of sources. Hence, I draw on examples from many disciplines and geographies. 

To become knowledge, our findings must be communicated to, understood, and trusted by other people. Scientific and economic progress can only be made by building on the work of others. And this is only possible if we can understand what they did. Similarly, if we are to create knowledge about the world, then we must enable others to understand precisely what we did, what we found, and how we went about our tasks. As such, in this book I will be particularly prescriptive about communication and reproducibility.

Improving the quality of quantitative work is an enormous challenge, yet it is the challenge of our time. Data are all around us, but there is little enduring knowledge being created. This book hopes to contribute, in some small way, to changing that.



## Audience and assumed background {-}

The typical person reading this book has some familiarity with first-year statistics, for instance they have run a regression. But it is not targeted at a particular level, instead providing aspects relevant to almost any quantitative course. I have taught from this book at high school, undergraduate, graduate, and professional, levels. Everyone has unique needs, but hopefully some aspect of this book speaks to you.

Enthusiasm and interest have taken folks far. If you have those, then do not worry about too much else. Some of the most successful students have been those with no quantitative or coding background. 

This book especially complements books such as: *Data Science: A First Introduction* [@timbersandfriends], *R for Data Science* [@r4ds], *An Introduction to Statistical Learning* [@islr], *Statistical Rethinking* [@citemcelreath], *Causal Inference: The Mixtape* [@Cunningham2021], *The Effect: An Introduction to Research Design and Causality* [@theeffect], and *Building Software Together* [@buildingsoftwaretogether]. If you are interested in those books, then this might be a good one to start with. 


## Structure and content {-}

This book is structured around six parts: I) Foundations, II) Communication, III) Acquisition, IV) Preparation, V) Modelling, and VI) Enrichment.

Part I -- Foundations -- begins with Chapter \@ref(telling-stories-with-data), which provides an overview of what I am trying to achieve with this book and why you should read it. Chapter \@ref(drinking-from-a-fire-hose) provides some worked examples. The intention of these is that you can experience the full workflow recommended in this book without worrying too much about the specifics of what is happening. That workflow is: plan, simulate, acquire, model, and communicate. It is normal to not follow everything in this chapter, but you should go through it, typing out and executing the code yourself. If you only have time to read one chapter of this book, then I recommend that one. Chapter \@ref(r-essentials) goes through some essential tasks in R, which is the statistical programming language used in this book. It is more of a reference chapter, and you may find yourself returning to it from time to time. And Chapter \@ref(reproducible-workflows) introduces some key tools for reproducibility used in the workflow that I advocate. These are things like using the command line, R Markdown, R Projects, Git and GitHub, and using R in practice.

Part II -- Communication -- considers three types of communication: written, static, and interactive. Chapter \@ref(on-writing) details the features that quantitative writing should have and how to go about writing a crisp, technical, paper. Static communication in Chapter \@ref(static-communication) introduces features like graphs, tables, and maps. Interactive communication in Chapter \@ref(interactive-communication) covers aspects such as websites, web applications, and maps that can be manipulated.

Part III -- Acquisition -- focuses on three aspects: farming data, gathering data, and hunting data. Farming data in Chapter \@ref(farm-data) begins with essential concepts from sampling that govern our approach to data. It then focuses on datasets that are explicitly provided for us to use as data, for instance censuses and other government statistics. These are typically clean, pre-packaged datasets, and sometimes complete. Gathering data in Chapter \@ref(gather-data) covers things like using Application Programming Interface (APIs), scraping data, getting data from PDFs, and Optical Character Recognition (OCR). The idea is that data are available, but not necessarily designed to be datasets, and that we must go and get them. Finally, hunting data in Chapter \@ref(hunt-data) covers aspects where more is expected of us. For instance, we may need to conduct an experiment, run an A/B test, or do some surveys. 

Part IV -- Preparation -- covers how to respectfully transform raw data into something that can be explored and shared. Chapter \@ref(clean-and-prepare) begins by detailing some principles to follow when approaching the task of cleaning and preparing data, and then goes through specific steps to take and checks to implement. Chapter \@ref(store-and-share) focuses on methods of storing and retrieving those datasets, including the use of R packages, and then continues onto considerations and steps to take when wanting to disseminate datasets as broadly as possible, while at the same time respecting those whose data they are based on.

Part V -- Modelling -- begins with exploratory data analysis in Chapter \@ref(exploratory-data-analysis). This is the critical process of coming to understand the nature of a dataset, but not something that typically finds itself into the final product. In Chapter \@ref(ijalm) the use of statistical models to explore data is introduced. Chapter \@ref(causality) is the first of three applications of modelling. It focuses on attempts to make causal claims from observational data and covers approaches such as difference-in-differences, regression discontinuity, and instrumental variables. Chapter \@ref(mrp) is the second of the modelling applications chapters and focuses on multilevel regression with post-stratification where we use a statistical model to adjust a sample for known biases. Chapter \@ref(text-as-data) is the third and final modelling application and is focused on text-as-data.

Part VI -- Enrichment -- introduces various next steps that would improve aspects of the workflow and approaches introduced in previous chapters. Chapter \@ref(using-the-cloud) which goes through moving away from your own computer and toward using the cloud. Chapter \@ref(deploying-models) discusses deploying models through the use of packages, web applications, and APIs. Chapter \@ref(efficiency) discusses various alternatives to the storage of data including feather and SQL; and also covers some ways to improve the performance of your code. Finally, Chapter \@ref(concludingremarks) offers some concluding remarks, details some open problems, and suggests some next steps.




## Pedagogy and key features {-}

You have to do the work. You should actively go through material and code yourself. As @stephenking says '[a]mateurs sit and wait for inspiration, the rest of us just get up and go to work'. Do not passively read this book. My role is best described by @hamming1996 [p. 2-3]:

> I am, as it were, only a coach. I cannot run the mile for you; at best I can discuss styles and criticize yours. You know you must run the mile if the athletics course is to be of benefit to you---hence you must think carefully about what you hear and read in this book if it is to be effective in changing you---which must obviously be the purpose...

This book is structured around a dense 12-week course. It provides enough material for advanced readers to be challenged, while establishing a core that all readers should master. Typically courses cover the material through to Chapter \@ref(ijalm), and then pick another couple of chapters that are of particular interest. 

From as early as Chapter \@ref(drinking-from-a-fire-hose) you will have a workflow---plan, simulate, acquire, model, and communicate---allowing you to tell a convincing story with data. In each subsequent chapter you will add aspects and depth to this workflow that will allow you to speak with increasing sophistication and credibility. As this workflow expands it addresses the skills that are typically sought in industry. For instance, features such as: communication, ethics, reproducibility, research question development, data collection, data cleaning, data protection and dissemination, exploratory data analysis, statistical modelling, and scaling.

One of the defining aspects of this book is that ethics and inequity concerns are integrated throughout, rather than being clustered in one, easily ignorable, chapter. These aspects are critical, yet it can be difficult to immediately see their value, hence their tight integration.

This book is also designed to enable you to build a portfolio of work that you could show to a potential employer. If you want an industry job, then this is arguably the most important thing that you should be doing. @robinsonnolis2020 [p. 55] describe how a portfolio is a collection of projects that show what you can do and is something that can help be successful in a job search.

In the novel *The Last Samurai* [@helendewitt p. 326], a character says:

> [A] scholar should be able to look at any word in a passage and instantly think of another passage where it occurred; ... [so a] text was like a pack of icebergs each word a snowy peak with a huge frozen mass of cross-references beneath the surface.

In an analogous way, this book not only provides you with text and instruction that is self-contained, but also helps develop critical masses of knowledge on which expertise is built. No chapter positions itself as the last word, instead they are written in relation to other work. 

Each chapter has the following features:

- A list of required materials that you should go through before you read that chapter. To be clear, you should first read that material and then return to this book. Each chapter also contains recommended materials for those who are particularly interested in the topic and want a starting place for further exploration. 
- A summary of the key concepts and skills that are developed in that chapter. Technical chapters additionally contain a list of the main packages and functions that are used in the chapter. The combination of these features acts as a checklist for your learning, and you should return to them after completing the chapter.
- A series of short exercises that you should complete after going through the required materials, but before going through the chapter, to test your knowledge. After completing the chapter, you should go back through the exercises to make sure that you understand each aspect. 
- One or two tutorial questions are included at the end of each chapter to further encourage you to actively engage with the material. You could consider forming small groups to discuss your answers to these questions.

Some chapters additionally feature:

- A section called 'Oh, you think we have good data on that!' which focuses on a particular setting, such as cause of death, in which it is often assumed that there is unimpeachable and unambiguous data but the reality tends to be quite far from that.
- A section called 'Shoulders of giants', which focuses on some of those who created the intellectual foundation on which we build.

Finally, a set of six papers is included in Appendix \@ref(papers). If you write these, you will be conducting original research on a topic that is of interest to you. Although open-ended research may be new to you, the extent to which you are able to: develop your own questions, use quantitative methods to explore them, and communicates your findings, is the measure of the success of this book.




## Software information and conventions {-}

The software that I use in this book is R [@citeR]. This language was chosen because it is open source, widely used, general enough to cover the entire workflow, yet specific enough to have plenty of well-developed features. I do not assume that you have used R before, and so another reason for selecting R for this book is the community of R users. The community is especially welcoming of new-comers and there is a lot of complementary beginner-friendly material available. There is an R package, `DoSSToolkit` [@alexander2021introduction], that contains `learnr` modules [@citelearnr]. This may be useful if you are newer to R and are especially complementary to this book.

If you do not have a programming language, then R is a great one to start with. If you have a preferred programming language already, then it wouldn't hurt to pick up R as well. That said, if you have a good reason to prefer another open-source programming language (for instance you use Python daily at work) then you may wish to stick with that. However, all examples in this book are in R.

Please download R and R Studio onto your own computer. You can download R for free here: http://cran.utstat.utoronto.ca/, and you can download R Studio Desktop for free here: https://rstudio.com/products/rstudio/download/#download. 
Please also create an account on R Studio Cloud: https://rstudio.cloud/. This will allow you to run R in the cloud.

Packages are in typewriter text, for instance, `tidyverse`, while functions are also in typewriter text, but include brackets, for instance `dplyr::filter()`.



## Acknowledgments {-}

Many people generously gave code, data, examples, guidance, opportunities, thoughts, and time, that helped develop this book.

Thank you to David Grubbs and the team at CRC Press for taking a chance on me and providing invaluable support.

Thank you to Michael Chong and Sharla Gelfand for greatly helping to shape some of the approaches I advocate. However, both do much more than that and contribute in an enormous way to the spirit of generosity that characterises the R community.

Thank you to Kelly Lyons for her support, guidance, mentorship, and friendship. Every day she demonstrates what an academic should be, and more broadly, what we should all aspire to be as a person.

Thank you to Greg Wilson for providing a structure to think about teaching, for being the catalyst for this book, and for helpful comments on drafts. Every day he provides an example of how to contribute to the intellectual community.

Thank you to an anonymous reviewer and Isabella Ghement, who thoroughly went through an early draft of this book and provided detailed feedback that improved this book.

Thank you to Hareem Naveed for helpful feedback and encouragement. Her industry experience was an invaluable resource as I grappled with questions of coverage and focus.

Thank you to Leslie Root, who came up with the idea around 'Oh, you think we have good data on that!'.

Thank you to my PhD supervisory panel John Tang, Martine Mariotti, Tim Hatton, and Zach Ward who gave me the freedom to explore the intellectual space that was of interest to me, the support to follow through on those interests, and the guidance to ensure that it all resulted in something tangible.

Thank you to Elle Côtè for enabling this book to be written.

This book has greatly benefited from the notes and teaching materials of others that are freely available online, especially: Chris Bail, Scott Cunningham, Andrew Heiss, Lisa Lendway, Grant McDermott, Nathan Matias, David Mimno, and Ed Rubin. Thank you to these folks. The changed norm of academics making their materials freely available online is a great one and one that I hope the free online version of this book helps contribute to.

Thank you to Samantha-Jo Caetano, who helped develop some of the assessment items. And also to Lisa Romkey and Alan Chong who allowed me to adapt some aspects of their rubric.

Thank you to those students who contributed substantially to the development of this book, including: A Mahfouz, Faria Khandaker, Keli Chiu, Paul Hodgetts, and Thomas William Rosenthal. I discussed most aspects of this book with them, and while they made specific contributions, they also changed and sharpened the way that I thought about almost everything covered here. Paul additionally made the art for this book.

Thank you to those students who identified specific improvements, including: Aaron Miller, Amy Farrow, Arsh Lakhanpal, Cesar Villarreal Guzman, Flavia López, Hong Shi, Laura Cline, Lorena Almaraz De La Garza, Mounica Thanam, Reem Alasadi, Wijdan Tariq, Yang Wu, and Yewon Han.

As at Christmas 2021 this book was a disparate collection of notes. Thank you to Mum and Dad, who dropped everything and came over from the other side world for two months to give me the opportunity to re-write it all, and put together a cohesive book.

Finally, thank you to Monica Alexander. Without you I would not have written a book; I would not have even thought it possible. Many of the best ideas in this book are yours, and those that are not, you made better. Thank you for your inestimable help with writing this book, providing the base on which it builds (remember in the library showing me many times how to get certain rows in R!), giving me the time that I needed to write, encouragement when it turned out that writing a book just meant endlessly re-writing that which was perfect the day before, reading everything in this book many times, making coffee or cocktails as appropriate, and more.

You can contact me at: rohan.alexander@utoronto.ca.

\BeginKnitrBlock{flushright}<p class="flushright">Rohan Alexander  
Toronto, Canada</p>\EndKnitrBlock{flushright}


