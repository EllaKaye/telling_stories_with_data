
# Store and share

**Required material**

- Read *Datasheets for datasets*, [@gebru2021datasheets].
- Read *Data and its (dis)contents: A survey of dataset development and use in machine learning research*, [@Paullada2021].
- Read *Ten simple rules for responsible big data research*, [@zook2017ten].
- Read *How Data Can Be Used Against People: A Classification of Personal Data Misuses*, [@kroger2021data].

**Key concepts and skills**

- FAIR principles for data sharing and management.
- Sharing data using: GitHub, R data packages, and depositing data.
- Data documentation and especially datasheets for datasets.
- Understanding what is personally identifying information, and how this depends on context.
- Implementing data simulation to share data.
- Know what differential privacy is and some of its likely effect on data science.

**Key libraries**

- `openssl` [@openssl]

**Key functions**

- `openssl::md5()`
- `openssl::sha512()`

## Introduction

After we have put together a dataset, an important part of being responsible is storing it appropriately and enabling easy retrieval. While it is certainly possible to be especially concerned about this, and entire careers are based on the storage and retrieval of data, to a certain extent, the baseline is not onerous. If we can get our dataset off our own computer, then we are much of the way there. Further confirming that someone else can retrieve it and use it, puts us much further than most.

That said, the FAIR principles are useful when we come to think more formally about data sharing and management. These are [@wilkinson2016fair]:

1. Findable. There is one, unchanging, identifier for the dataset and the dataset has high-quality descriptions and explanations.
2. Accessible. Standardized approaches can be used to retrieve the data, and these are open and free, possibly with authentication, and that the metadata persists even if the dataset is removed.
3. Interoperable. The dataset and its metadata use a broadly applicable language, and vocabulary.
4. Reusable. There is plenty of description of the dataset and the usage conditions are made clear along with provenance.

It is important to recognize that just because a dataset is FAIR, it is not necessarily an unbiased representation of the world. FAIR reflects whether a dataset is appropriately available, not whether it is appropriate.


One reason for the rise of data science is that humans are at the heart of it. And often the data that we are interested in directly concern humans. This means there is a tension between sharing the data to facilitate reproducibility and maintaining privacy. Medicine has developed approaches to this over a long time. And out of that we have seen Health Insurance Portability and Accountability Act (HIPAA) in the US, and the related General Data Protection Regulation (GDPR) in Europe. Our concerns in data science tend to be about personally identifying information (PII). We have a variety of ways to protect especially private information in our datasets, such as emails, including hashing. And sometimes we simulate data and distribute that instead of sharing the actual dataset. More recently, differential privacy is being implemented. But this is usually an inappropriate choice, for anything other than the most massive of datasets and ensures a level of privacy, only at the expense of population minorities.

In this chapter we will consider how we plan and organize our datasets to meet essential requirements. To a large extent we put these in place to make our own life easier when we come back to use our dataset later. We then go through putting our dataset on GitHub, building R packages for data, and finally depositing it in various archives. Then we consider documentation, and in particular focus on datasheets.


## Plan

The storage and retrieval of information has a long history. This is especially connected with libraries which have existed since antiquity and have established protocols for deciding what information to store and what to discard, as well as its retrieval. One of the defining aspects of libraries is that deliberate curation and organization. The cataloging system ensures that books on similar topics are located close to each other, and there are typically also deliberate plans for ensuring the collection is up-to-date.

Vannevar Bush defines a 'memex' in 1945 as a device used to store books, records, and communications, in a way that supplements memory [@vannevarbush]. And the key is the indexing, or linking together of items. We can see this concept echoed in Tim Berners-Lee proposal for hypertext [@berners1989information], which led to the World Wide Web. This is the way that resources are identified. They are then transported over the Internet, using HTTP.

At its most fundamental, this is about storing and retrieving data. For instance, we make various files on our computer available to others. The internet is famously brittle, but when we are considering the storage and retrieval of our datasets we want to consider especially, for how long it is important that the data are stored and for whom [@michener2015ten]. For instance, if we want some data to be available for a decade and widely available then it becomes important to store data in open and persistent formats, such as CSVs [@hart2016ten]. But if we are just using some data as part of an intermediate step, we have the raw data, and the scripts to create it, then it might be fine to not worry too much about such considerations.

Storing raw data is important and there are many cases where raw data have revealed or hinted at fraud [@simonsohn2013just]. Shared data also enhances the credibility of our work, by enabling others to verify it, and can lead to the generation of new knowledge as others use it to answer different questions [@christensen2019transparent]. Finally, research that shares its data may be more highly cited [@christensen2019study].



## Share data

### GitHub

The easiest place to store our datasets will be GitHub because that is already built into our workflow. For instance, when we push, our dataset becomes available. One great benefit of this is that, if we have set-up our workspace appropriately, then we likely store our raw data, and the tidy data, as well as the scripts that are needed to transform one to the other. 

As an example of how we have stored some data, we can access the 'raw_data.csv' file from the 'starter_folder'. To get the file that we pass to `read_csv()` we navigate to the file in GitHub, and then click 'Raw'.


```r
library(tidyverse)

starter_data <- read_csv("https://raw.githubusercontent.com/RohanAlexander/starter_folder/main/inputs/data/raw_data.csv")

starter_data
#> # A tibble: 1 × 3
#>   first_col second_col third_col
#>   <chr>     <chr>      <chr>    
#> 1 some      raw        data
```

One issue with this is that the dataset does not have much documentation. While we can store and retrieve the dataset easily in this way, it lacks much explanation, a formal dictionary, and aspects such as a license that would bring our dataset closer to aligning with the FAIR principles.




### R Packages for data

To this point we have largely used R packages for their code, although we have seen a few that were focused on sharing data, for instance, @troopdata. We can build an R Package for our dataset and then add it to GitHub. This will make it easy to store and retrieve because we can obtain the dataset by loading the package. This will be the first R package that we build. In Chapter \@ref(deploying-models), will return to R packages and use them to deploy models.

To get started, create a new package ('File' -> 'New project' -> 'New Directory' -> 'R Package'). Give the package a name, such as 'favcolordata' and select 'Open in new session'. Create a new folder called 'data'. We will simulate a dataset that we will include.


```r
library(tidyverse)

set.seed(853)

color_data <-
    tibble(
        name =
            c("Edward",
              "Helen",
              "Hugo",
              "Ian",
              "Monica",
              "Myles",
              "Patricia",
              "Roger",
              "Rohan",
              "Ruth"
            ),
        fav_color =
            sample(
                x = c("Black", "White", "Rainbow"),
                size = 10,
                replace = TRUE
            )
    )
```

To this point we have largely been trying to use CSV files for our datasets. To include our data in this R package, we will save our dataset in a particular format, 'rda', using `save()`.


```r
save(color_data, file="data/color_data.rda")
```

Then create an R file 'data.R' in the 'R' folder. This R file will only contain documentation using `roxygen2` comments, which start with `#'`, and we follow the documentation for `troopdata` closely.


```r
#' Favorite color of various people data
#'
#' @description \code{favcolordata} returns a dataframe of the favorite color of various people.
#' 
#' @return Returns a dataframe of the favorite color of various people.
#' 
#' @docType data
#'
#' @usage data(color_data)
#'
#' @format An dataframe of individual-level observations with the following variables: 
#'
#' \describe{
#' \item{\code{name}}{A character vector of individual names.}
#' \item{\code{fav_color}}{A character vector of one of: black, white, rainbow.}
#' }
#'
#' @keywords datasets
#'
#' @source \url{https://www.tellingstorieswithdata.com/storing-and-retrieving-data.html}
#'
"color_data"

```

Finally, we should add a README which provides a summary of all of this for someone coming to the project from the outside.

At this we can go to the 'Build' tab and then 'Install and Restart'. After this happens, the package 'favcolordata', is loaded and the data can be accessed using 'color_data'. If we were to push this to GitHub, then anyone would be able to install the package using `devtools` [@citeDevtools] and then use our dataset.


```r
devtools::install_github("RohanAlexander/favcolordata")

library(favcolordata)

color_data
```

This has addressed many of the issues that we faced earlier. For instance, we have included a README and a data dictionary of sorts in terms of the descriptions that we added. But if we were to try to put this package onto CRAN, then we might face some issues. For instance, the maximum size of a package is 5MB and we would quickly come up against that. We have also largely forced users to use R, and while there are considerable benefits of that, we may like to be more language agnostic [@tierney2020realistic].


### Depositing data

While it is possible that a dataset will be cited if it is available through GitHub or an R package, this becomes more likely if the dataset is deposited somewhere. There are several reasons for this, but one is that it seems a bit more formal. Zenodo and Open Science Framework (OSF) are two that are commonly used. For instance, @chris_carleton_2021_4550688 use Zenodo to share the dataset and analysis supporting @carleton2021reassessment. Similarly @geuenich_michael_2021_5156049 use Zenodo to share the dataset that underpins @geuenich2021automated.
<!-- And Y use OSF to share all files. -->

Another option is a dataverse, such as the Harvard Dataverse, which is a common requirement for journal publications. One nice aspect of this is that we can use `dataverse` [@dataverse] to retrieve the dataset as part of a reproducible workflow.


## Documentation

Datasheets [@gebru2021datasheets] are an increasingly critical aspect of data science. Datasheets are basically nutrition labels for datasets. The process of creating them enables us to think more carefully about what we will feed our model. More importantly, they enable others to better understand what we fed our model. One important task is going back and putting together datasheets for datasets that are widely used. For instance, researchers went back and wrote a datasheet for one of the most popular datasets in computer science, and they found that around 30 per cent of the data were duplicated [@bandy2021addressing].

Instead of telling us how unhealthy various foods are, a datasheet tells us things like:

- Who put the dataset together?
- Who paid for the dataset to be created?
- How complete is the dataset?
- What fields are present, and equally not present, for particular observations?

Sometimes we have done a lot of work to create a dataset. In that case, we may like to publish and share it on its own, for instance, @biderman2022datasheet and @bandy2021addressing. But typically a datasheet might live in an appendix to the paper, or be included in a file adjacent to the dataset.

We will put together a datasheet for the dataset that underpins @citeaustralianpoliticians. The text of the questions directly comes from @gebru2021datasheets. When we create datasheets for a dataset, especially a dataset that we did not put together ourselves, it is possible that the answer to some questions will simply be "Unknown".

**Motivation**

1. *For what purpose was the dataset created? Was there a specific task in mind? Was there a specific gap that needed to be filled? Please provide a description.*
    - The dataset was created to enable analysis of Australian politicians. We were unable to find a publicly available dataset in a structured format that had the biographical and political information on Australian politicians that was needed for modelling.
2. *Who created the dataset (for example, which team, research group) and on behalf of which entity (for example, company, institution, organization)?*
    - Rohan Alexander, while working at the Australian National University and the University of Toronto
3. *Who funded the creation of the dataset? If there is an associated grant, please provide the name of the grantor and the grant name and number.*
    - No direct funding was received for this project, but Rohan received a salary from University of Toronto.
4. *Any other comments?*
    - No.

**Composition**

1. *What do the instances that comprise the dataset represent (for example, documents, photos, people, countries)? Are there multiple types of instances (for example, movies, users, and ratings; people and interactions between them; nodes and edges)? Please provide a description.*
	- Each row of the main dataset is an individual, and these then link to other datasets where each row refers to various information about that person.
2. *How many instances are there in total (of each type, if appropriate)?*
	- A little more than 1700.
3. *Does the dataset contain all possible instances or is it a sample (not necessarily random) of instances from a larger set? If the dataset is a sample, then what is the larger set? Is the sample representative of the larger set (for example, geographic coverage)? If so, please describe how this representativeness was validated/verified. If it is not representative of the larger set, please describe why not (for example, to cover a more diverse range of instances, because instances were withheld or unavailable).*
	- All individuals elected or appointed to the Australian Federal Parliament are in the dataset.
4. *What data does each instance consist of? "Raw" data (for example, unprocessed text or images) or features? In either case, please provide a description.*
	- Each instance consists of biographical information such as birthdate, or political information, such as political party membership.
5. *Is there a label or target associated with each instance? If so, please provide a description.*
	- Yes there is a unique key comprising the surname and year of birth, with a few individuals needing additional demarcation.
6. *Is any information missing from individual instances? If so, please provide a description, explaining why this information is missing (for example, because it was unavailable). This does not include intentionally removed information, but might include, for example, redacted text.*
	- Birthdate is not available in all cases, especially earlier in the dataset.
7. *Are relationships between individual instances made explicit (for example, users' movie ratings, social network links)? If so, please describe how these relationships are made explicit.*
	- Yes, through the uniqueID.
8. *Are there recommended data splits (for example, training, development/validation, testing)? If so, please provide a description of these splits, explaining the rationale behind them.*
	- No.
9. *Are there any errors, sources of noise, or redundancies in the dataset? If so, please provide a description.*
	- There is some uncertainty about cabinet and ministries. For instance, different sources differ. There is also a little bit of uncertainty about birthdates.
10. *Is the dataset self-contained, or does it link to or otherwise rely on external resources (for example, websites, tweets, other datasets)? If it links to or relies on external resources, a) are there guarantees that they will exist, and remain constant, over time; b) are there official archival versions of the complete dataset (that is, including the external resources as they existed at the time the dataset was created); c) are there any restrictions (for example, licenses, fees) associated with any of the external resources that might apply to a dataset consumer? Please provide descriptions of all external resources and any restrictions associated with them, as well as links or other access points, as appropriate.*
	- Self-contained.
11. *Does the dataset contain data that might be considered confidential (for example, data that is protected by legal privilege or by doctor-patient confidentiality, data that includes the content of individuals' non-public communications)? If so, please provide a description.*
	- No, all data were gathered from public sources.
12. *Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety? If so, please describe why.*
	- No.
13. *Does the dataset identify any sub-populations (for example, by age, gender)? If so, please describe how these subpopulations are identified and provide a description of their respective distributions within the dataset.*
	- Yes, age and gender.
14. *Is it possible to identify individuals (that is, one or more natural persons), either directly or indirectly (that is, in combination with other data) from the dataset? If so, please describe how.*
	- Yes, individuals are identified by name.
15. *Does the dataset contain data that might be considered sensitive in any way (for example, data that reveals race or ethnic origins, sexual orientations, religious beliefs, political opinions or union memberships, or locations; financial or health data; biometric or genetic data; forms of government identification, such as social security numbers; criminal history)? If so, please provide a description.*
	- The dataset contains sensitive information, such as political membership, however this is all public knowledge as they are federal politicians.
16. *Any other comments?*
	- No.

**Collection process**

1. *How was the data associated with each instance acquired? Was the data directly observable (for example, raw text, movie ratings), reported by subjects (for example, survey responses), or indirectly inferred/derived from other data (for example, part-of-speech tags, model-based guesses for age or language)? If the data was reported by subjects or indirectly inferred/derived from other data, was the data validated/verified? If so, please describe how.*
	- The data were gathered from the Australian Parliamentary Handbook in the first instance, and this was augmented with information from other parliaments, especially Victoria and New South Wales, and Wikipedia.
2. *What mechanisms or procedures were used to collect the data (for example, hardware apparatuses or sensors, manual human curation, software programs, software APIs)? How were these mechanisms or procedures validated?*
	- Scraping and parsing using R.
3. *If the dataset is a sample from a larger set, what was the sampling strategy (for example, deterministic, probabilistic with specific sampling probabilities)?*
	- The dataset is not a sample.
4. *Who was involved in the data collection process (for example, students, crowdworkers, contractors) and how were they compensated (for example, how much were crowdworkers paid)?*
	- Rohan Alexander. Paid as a post-doc and an assistant professor, although this was not tied to this specific project.
5. *Over what timeframe was the data collected? Does this timeframe match the creation timeframe of the data associated with the instances (for example, recent crawl of old news articles)? If not, please describe the timeframe in which the data associated with the instances was created.*
	- Three years, and then updated from time to time.
6. *Were any ethical review processes conducted (for example, by an institutional review board)? If so, please provide a description of these review processes, including the outcomes, as well as a link or other access point to any supporting documentation.*
	- No.
7. *Did you collect the data from the individuals in question directly, or obtain it via third parties or other sources (for example, websites)?*
	- Third parties in almost all cases.
8. *Were the individuals in question notified about the data collection? If so, please describe (or show with screenshots or other information) how notice was provided, and provide a link or other access point to, or otherwise reproduce, the exact language of the notification itself.*
	- No.
9. *Did the individuals in question consent to the collection and use of their data? If so, please describe (or show with screenshots or other information) how consent was requested and provided, and provide a link or other access point to, or otherwise reproduce, the exact language to which the individuals consented.*
	- No.
10. *If consent was obtained, were the consenting individuals provided with a mechanism to revoke their consent in the future or for certain uses? If so, please provide a description, as well as a link or other access point to the mechanism (if appropriate).*
	- Consent was not obtained.
11. *Has an analysis of the potential impact of the dataset and its use on data subjects (for example, a data protection impact analysis) been conducted? If so, please provide a description of this analysis, including the outcomes, as well as a link or other access point to any supporting documentation.*
	- No.
12. *Any other comments?*
	- No.

**Preprocessing/cleaning/labeling**

1. *Was any preprocessing/cleaning/labeling of the data done (for example, discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)? If so, please provide a description. If not, you may skip the remaining questions in this section.*
	- Yes cleaning of the data was done.
2. *Was the "raw" data saved in addition to the preprocessed/cleaned/labeled data (for example, to support unanticipated future uses)? If so, please provide a link or other access point to the "raw" data.*
	- In general, no. The scripts that got the data from the parliamentary handbook to CSV are not available. There are scripts that go through Wikipedia and check things and these are available.
3. *Is the software that was used to preprocess/clean/label the data available? If so, please provide a link or other access point.*
	- R was used.
4. *Any other comments?*
	- No

**Uses**

1. *Has the dataset been used for any tasks already? If so, please provide a description.*
	- Yes, a few papers about Australian politics, for instance, https://arxiv.org/abs/2111.09299.
2. *Is there a repository that links to any or all papers or systems that use the dataset? If so, please provide a link or other access point.*
	- No
3. *What (other) tasks could the dataset be used for?*
	- Linking with elections would be interesting.
4. *Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses? For example, is there anything that a dataset consumer might need to know to avoid uses that could result in unfair treatment of individuals or groups (for example, stereotyping, quality of service issues) or other risks or harms (for example, legal risks, financial harms)? If so, please provide a description. Is there anything a dataset consumer could do to mitigate these risks or harms?*
	- No.
5. *Are there tasks for which the dataset should not be used? If so, please provide a description.*
	- No.
6. *Any other comments?*
	- No.

**Distribution**

1. *Will the dataset be distributed to third parties outside of the entity (for example, company, institution, organization) on behalf of which the dataset was created? If so, please provide a description.*
	- The dataset is available through GitHub.
2. *How will the dataset be distributed (for example, tarball on website, API, GitHub)? Does the dataset have a digital object identifier (DOI)?*
	- GitHub for now, and eventually a deposit.
3. *When will the dataset be distributed?*
	- The dataset is available now.
4. *Will the dataset be distributed under a copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)? If so, please describe this license and/ or ToU, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms or ToU, as well as any fees associated with these restrictions.*
	- No. MIT license.
5. *Have any third parties imposed IP-based or other restrictions on the data associated with the instances? If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any relevant licensing terms, as well as any fees associated with these restrictions.*
	- None that are known.
6. *Do any export controls or other regulatory restrictions apply to the dataset or to individual instances? If so, please describe these restrictions, and provide a link or other access point to, or otherwise reproduce, any supporting documentation.*
	- None that are known.
7. *Any other comments?*
	- No.

**Maintenance**

1. *Who will be supporting/hosting/maintaining the dataset?*
	- Rohan Alexander
2. *How can the owner/curator/manager of the dataset be contacted (for example, email address)?*
	- rohan.alexander@utoronto
3. *Is there an erratum? If so, please provide a link or other access point.*
	- No, the dataset is just updated.
4. *Will the dataset be updated (for example, to correct labeling errors, add new instances, delete instances)? If so, please describe how often, by whom, and how updates will be communicated to dataset consumers (for example, mailing list, GitHub)?*
	- Yes, roughly quarterly.
5. *If the dataset relates to people, are there applicable limits on the retention of the data associated with the instances (for example, were the individuals in question told that their data would be retained for a fixed period of time and then deleted)? If so, please describe these limits and explain how they will be enforced.*
	- No.
6. *Will older versions of the dataset continue to be supported/hosted/maintained? If so, please describe how. If not, please describe how its obsolescence will be communicated to dataset consumers.*
	- No the dataset is just updated. Although a history is available through GitHub.
7. *If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for them to do so? If so, please provide a description. Will these contributions be validated/verified? If so, please describe how. If not, why not? Is there a process for communicating/distributing these contributions to dataset consumers? If so, please provide a description.*
	- Pull request on GitHub.
8. *Any other comments?*
	- No

## Personally identifying information

Personally identifying information (PII) is that which enables us to link a row in our dataset with an actual person. For instance, email addresses are often PII, as are names and addresses. Interestingly, sometimes the combination of several variables, none of which are PII in and of themselves, can be PII. For instance, age is unlikely PII by itself, but age combined with city, education, and a few other variables could be. One concern is that this re-identification can occur across datasets. Another interesting aspect is that again while some variable may not be PII for almost everyone in the dataset, it can become PII in the extreme. For instance, if we have age, then there are many people of most ages, but there are fewer people in ages over 100 and it likely becomes PII. The same scenario happens with both income and wealth. One response to this is for data to be censored. For instance, we may record age between 0 and 100, and then group everyone over that into '101+'.

@zook2017ten recommend considering whether data even need to be gathered in the first place. For instance, if a phone number is not absolutely required then it might be better to not gather it in the first place, rather than need to worry about protecting it before data dissemination.


GDPR and HIPAA are two legal structures that govern data in Europe and the US, respectively. Due to the influence of these regions, they have a significant effect outside those regions also. GDPR concerns data generally, while HIPAA is focused on healthcare. GDPR applies to all personal data, which is defined as:

> 'personal data' means any information relating to an identified or identifiable natural person ('data subject'); an identifiable natural person is one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or to one or more factors specific to the physical, physiological, genetic, mental, economic, cultural or social identity of that natural person;
>
> @gdpr, Article 4, 'Definitions'

HIPAA refers to the privacy of medical records in the US and codify the idea that the patient should have access to their medical records, and that only the patient should be able to authorize access to their medical records [@annas2003hipaa]. While it only applies to covered entities, it sets a standard that informs practice, yet is piecemeal given the variety of applications. For instance, a person's social media posts about their health is generally not subject to it, nor is knowledge about a person's location and how active they are, even though based on that information we may be able to get some idea of their health [@Cohen2018]. Such data are hugely valuable [@ibmdataset].

There are a variety of ways of protecting PII, while sharing data, that we will now go through.

### Hashing and salting

A hash is a one-way transformation of data, such that the same input always provides the same output, but given the output, it is not reasonably possible to obtain the input. For instance, a function that doubled its input always gives the same output, for the same input, but is also easy to reverse. 

@knuth [p. 514] relates an interesting etymology for 'hash' by first defining 'to hash' as relating to chop up or make a mess, and then explaining that hashing relates to scrambling the input and using this partial information to define the output. A collision is when different inputs map to the same output, and one feature of a good hashing algorithm is that collisions are reduced. One simple approach is to rely on the modulo operator. For instance, if we were interested in 10 different groupings for the integers 1 through to 10. A better approach would be for the number of groupings to be a prime number, such as 11 or 853.


```r
library(tidyverse)

hashing <- 
  tibble(ppi_data = c(1:10),
         modulo_ten = ppi_data %% 10,
         modulo_eleven = ppi_data %% 11,
         modulo_eightfivethree = ppi_data %% 853)

hashing
#> # A tibble: 10 × 4
#>    ppi_data modulo_ten modulo_eleven modulo_eightfivethree
#>       <int>      <dbl>         <dbl>                 <dbl>
#>  1        1          1             1                     1
#>  2        2          2             2                     2
#>  3        3          3             3                     3
#>  4        4          4             4                     4
#>  5        5          5             5                     5
#>  6        6          6             6                     6
#>  7        7          7             7                     7
#>  8        8          8             8                     8
#>  9        9          9             9                     9
#> 10       10          0            10                    10
```

Rather than worry about things ourselves, we can use various hash functions from `openssl` [@openssl] including `sha512()` and `md5()`.


```r
library(openssl)

openssl_hashing <- 
  tibble(names =
            c("Edward",
              "Helen",
              "Hugo",
              "Ian",
              "Monica",
              "Myles",
              "Patricia",
              "Roger",
              "Rohan",
              "Ruth"
            )) |> 
  mutate(md5 = md5(names),
         sha512 = sha512(names)
  )

openssl_hashing
#> # A tibble: 10 × 3
#>    names    md5                              sha512         
#>    <chr>    <hash>                           <hash>         
#>  1 Edward   243f63354f4c1cc25d50f6269b844369 5759ada975e7cb…
#>  2 Helen    29e00d3659d1c5e75f99e892f0c1a1f1 6ee4156ca7e8e9…
#>  3 Hugo     1b3840b0b70d91c17e70014c8537dbba b1e441a5486690…
#>  4 Ian      245a58a5dc42397caf57bc06c2c0afd2 d3cf9cdaea6ffd…
#>  5 Monica   09084cc0cda34fd80bfa3cc0ae8fe3dc 84250b971b8772…
#>  6 Myles    fafdf519cb5877d4751b4cbe6f3f534a 4eae7c19d5c5d4…
#>  7 Patricia 54a7b18f26374fc200ddedde0844f8ec e511593a2db805…
#>  8 Roger    efc5c58b9a85926a31587140cbeb0220 f63ab236a5b013…
#>  9 Rohan    02df8936eee3d4d2568857ed530671b2 5111e18391d41f…
#> 10 Ruth     8e06843ec162b74a7902867dd4bca8c8 d7e7d23b69e372…
```

We could share either of these and be comfortable that, in general, it would be difficult for someone to use only that information to recover the names of our respondents. That is not to say that it is impossible. If we made a mistake, such as accidentally committing the original dataset to GitHub then they could be recovered. And of course, it is likely that various governments have the ability to reverse the cryptographic hashes used here.

One issue that remains is that anyone can take advantage of the key feature of hashing being that the same input always gets the same output, to test various options for inputs. For instance, they could, themselves try to has 'Rohan', and then noticing that the hash is the same as the one that we published in our dataset, know that data relates to that particular individual. We could try to keep our hashing approach secret, but that is difficult as there are only a few that was widely used. One approach is to add a salt that we keep secret. This slightly changes the input. For instance, we could add the salt '_is_a_person' to all our names and then hash that, although a large random number might be a better option. Provided the salt is not shared, then it would be difficult for most folks to reverse our approach in that way.


```r
openssl_hashing_with_salt <- 
  tibble(names =
            c("Edward",
              "Helen",
              "Hugo",
              "Ian",
              "Monica",
              "Myles",
              "Patricia",
              "Roger",
              "Rohan",
              "Ruth"
            )
         ) |> 
  mutate(names = paste0(names, "_is_a_person")) |> 
  mutate(md5 = md5(names),
         sha512 = sha512(names)
         )

openssl_hashing_with_salt
#> # A tibble: 10 × 3
#>    names                md5                           sha512
#>    <chr>                <hash>                        <hash>
#>  1 Edward_is_a_person   9845500d4070c0cbba7c6b81ed30… e8ce0…
#>  2 Helen_is_a_person    7e4a77b41fb6e108618f93fb9f47… b066b…
#>  3 Hugo_is_a_person     b9b8c4e9870aca482cf062da4681… 07c18…
#>  4 Ian_is_a_person      9b1ad8fbbc190c2e3ce74372029f… eb992…
#>  5 Monica_is_a_person   50bb9dfffa926c855b830845ac61… ef429…
#>  6 Myles_is_a_person    3635be5fe758ed1fc0d9c78fc0b2… 795dc…
#>  7 Patricia_is_a_person 4e4a5ed8842fd7caad320c3a92bf… 1b446…
#>  8 Roger_is_a_person    ea1d56e89771d8b0a7b598132442… 2f753…
#>  9 Rohan_is_a_person    3ab064d7f746fde604122d072fd4… cc9c7…
#> 10 Ruth_is_a_person     8b83f4285ac30a3efa5ede3636b7… 6d329…
```


### Data simulation

One common approach to deal with the issue of being unable to share the actual data that underpins an analysis, is to use data simulation. We have used data simulation throughout this book toward the start of the workflow to help us to think more deeply about our dataset before we turn to it. We can use data simulation again at the end, to ensure that others cannot think about our actual dataset. The workflow advocated in this book makes this relatively straight-forward.

The approach is to understand the critical features of the dataset and the appropriate distribution. For instance, if our data were the ages of some population, then we may want to use the Poisson distribution and experiment with different parameters for lambda. Having simulated a dataset, we conduct our analysis using this simulated dataset and ensure that the results are broadly similar to when we use the real data. We can then release the simulated dataset along with our code.

For more nuanced situations, @koenecke2020synthetic recommend using the synthetic data vault [@patki2016synthetic] and then the use of Generative Adversarial Networks, such as implemented by @athey2021using.



### Differential privacy

Differential privacy implements a mathematical definition of privacy, that means that even if datasets are combined, a certain level of privacy will be maintained. A dataset is differentially private to different levels, based on how much it changes when one person's results are removed.

A variant of differential privacy has recently been implemented by the US census. This has been shown to not universally protect respondent privacy, and yet it is expected to have a significant effect on redistricting [@kenny2021impact]. @Suriyakumar2021 found that such model will be disproportionately affected by large demographic groups. The implementation of differential privacy is expected to result in publicly available data that are unusable in the social sciences [@ruggles2019differential].




## Exercises and tutorial


### Exercises

1. Following @wilkinson2016fair, which of the following are FAIR principles (please select all that apply)?
    a. Findable.
    b. Approachable.
    c. Interoperable.
    d. Reusable.
    e. Integrated.
    f. Fungible.
    g. Reduced.
    h. Accessible.
2. Please create an R package for a simulated dataset, push it to GitHub, and submit the link.
3. Please simulate some data, add it to a GitHub repository and then submit the link.
4. According to @gebru2021datasheets, a datasheet should document a dataset's (please select all that apply):
    a. composition.
    b. recommended uses.
    c. motivation.
    d. collection process.
5. Do you think that a person's name is PII? 
  a.  Yes.
  b. No.
6. Under what circumstances do you think income is PII (please write a paragraph or two)?
7. Using `openssl::md5()` what is the hash of "Rohan" (pick one)?
    a. 243f63354f4c1cc25d50f6269b844369
    b. 09084cc0cda34fd80bfa3cc0ae8fe3dc
    c.  02df8936eee3d4d2568857ed530671b2
    d. 1b3840b0b70d91c17e70014c8537dbba


### Tutorial

Please identify a dataset you consider interesting and important, that does not have a datasheet [@gebru2021datasheets]. As a reminder, datasheets accompany datasets and document 'motivation, composition, collection process, recommended uses,' among other aspects. Please put together a datasheet for this dataset. You are welcome to use the template [here](https://github.com/RohanAlexander/starter_folder/blob/main/inputs/data/datasheet_template.Rmd) as a starting point. The datasheet should be completely contained in its own GitHub repository. Please submit a PDF.


### Paper

At about this point, Paper Four (Appendix \@ref(paper-four)) would be appropriate.




<!-- Look into how IQ tests are conducted and what goes into them. To what extent do you think they measure intelligence? Some aspects that you may like to think about in answering that question include: Who decides what is intelligence? How is this updated? What is missing from that definition? To what extent is this generalisable? You should write a page or two. -->








<!-- The purpose of this tutorial is to ensure that it is clear in your mind how thoroughly you should know your dataset. It builds on the 'memory palace' technique used by professional memorisers, as described by @moonwalkingwitheinstein. -->

<!-- Please think about your childhood home, or another building that you know intimately. Imagine yourself standing at the front of it. Describe what it looks like. Then 'walk' into the front and throughout the house, again describing each aspect in as much detail as you can imagine. What are each of the rooms used for and what are their distinguishing features? How does it smell? What does this all evoke in you? Please write a page or two.  -->

<!-- Now think about a dataset that you are interested in. Please do this same exercise, but for the dataset. -->


