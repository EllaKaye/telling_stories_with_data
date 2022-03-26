
# (PART) Enrichment {-}

# Deploying models

**Required reading**

- Read *Machine learning is going real-time*, [@chiphuyenone].
- Read *Real-time machine learning: challenges and solutions*, [@chiphuyentwo].
- Watch *Democratizing R with Plumber APIs*, [@democratizingr].



<!-- **Required viewing** -->

<!-- . -->
<!-- - Nolis, Heather, and Jacqueline Nolis, 'We are hitting R a million times a day so we made a talk about it', RStudio Conference, 30 January, https://www.rstudio.com/resources/rstudioconf-2020/we-re-hitting-r-a-million-times-a-day-so-we-made-a-talk-about-it/. -->


<!-- **Recommended reading** -->

<!-- - Edmondson, Mark, 2020, 'googleComputeEngineR documentation', version 0.3.0.9000, freely available at: https://cloudyr.github.io/googleComputeEngineR/. -->
<!-- - McDermott, Grant R., 2020, 'Cloud computing with Google Compute Engine', *Data Science for Economists*, freely available at: https://raw.githack.com/uo-ec607/lectures/master/14-gce/14-gce.html. -->
<!-- - Morris, Mitzi, 2020, 'Stan Notebooks in the Cloud', freely available at: https://mc-stan.org/users/documentation/case-studies/jupyter_colab_notebooks_2020.html. -->


**Key concepts and skills**

- Benefits/costs of cloud.
- Getting started in the cloud.
- Starting virtual machines with R Studio.
- Stopping virtual machines.
- Putting models into production requires a different set of skills to building a model. We need a familiarity with some cloud provider, APIs, and of course modelling. But the biggest difficulty, for me, is getting things set-up.


**Key libraries**

- `plumber` [@plumber]
- `shiny` [@citeshiny]

## Introduction

Having done the work to develop a dataset and explore it with a model that we are confident can be used, we may wish to enable this to be used more widely thank just our own computer. There are a variety of ways of doing this, including:

- using the cloud,
- creating R packages,
- making `shiny` applications, and
- using `plumber` to create an API.

The general idea here is that we need to know, and allow others to come to trust, the whole workflow. That is what our approach to this point brings. After this, then we may like to use our model more broadly. Say we been able to scrape some data from a website, bring some order to that chaos, make some charts, appropriately model it, and write this all up. In most academic settings that is more than enough. But in many industry settings we would like to use the model to do something. For instance, setting up a website that allows a model to be used to generate an insurance quote given several inputs.

In this chapter, we begin by moving our compute from our local computer to the cloud. We then describe the use of R packages and Shiny for sharing models. That works well, but in some settings other users may like to interact with our model in ways that we are not focused on. One way to allow this is to make our results available to other computers, and for that we will want to make an APIs. Hence, we introduce `plumber` [@plumber], which is a way of creating APIs.




## Amazon Web Services

The apocryphal quote is that the cloud is another name for someone else's computer. And while that is true to various degrees, for our purposes that is enough. Learning to use someone else's computer can be great for a number of reasons including:

1) Scalability: It can be quite expensive to buy a new computer, especially if we only need it to run something every now and then, but by using someone else's computer, we can just rent for a few hours or days. This allows use to amortize this cost and work out what we actually need before committing to a purchase. It also allows us to easily increase or decrease the compute scale if we suddenly have a substantial increase in demand.
2) Portability: If we can shift our analysis workflow from a local machine to the cloud, then that suggests that there is we are likely doing good things in terms of reproducibility and portability. At the very least, code can run both locally and on the cloud, which is a big step in terms of reproducibility.
3) Set-and-forget: If we are doing something that will take a while, then it can be great to not have to worry about our own computer needing to run overnight, or, say, not being able to watch Netflix on that same computer. Additionally, on many cloud options, open-source statistical software, such as R and Python, is either already available, or relatively easy to set-up.

That said, there are downsides, including:

- Cost: While most cloud options are cheap, they are rarely free. To provide an idea of cost, using a well-featured AWS instance for a few days, may end up being a few dollars. It is also easy to accidentally forget about something, and generate unexpectedly large bills, especially initially. 
- Public: It can be easy to make mistakes and accidentally make everything public.
- Time: It takes time to get set-up and comfortable on the cloud.

When we use the cloud, we are typically running code on a 'virtual machine' (VM). This is an allocation that is part of a larger collection of computers that has been designed to act like a computer with specific features. For instance, we may specify that our virtual machine has, say, 8 GB RAM, 128 storage, and 4 CPUs. The VM would then act like a computer with those specifications. The cost to use cloud options increases based on the specifications of the virtual machine.

In a sense, we started with a cloud option, through our initial recommendation, in Chapter \@ref(drinking-from-a-fire-hose) of using R Studio Cloud, before we moved to our local machine in Chapter \@ref(r-essentials). That cloud option was specifically designed for beginners. We will now introduce 
<!-- two additional options, which enable substantial scaling. Google Colab, which we introduce as a pre-cursor to Python. And then moving to  -->
a more general cloud option: Amazon Web Services (AWS). Often a particular business will use a particular cloud option, such as Google, AWS, or Azure, but developing familiarity with one will make the use of the others easier.

<!-- ### Google Colab -->

<!-- Google Colab is similar to R Studio Cloud, in that it is set-up to allow us to just log in and get started. In this case, we need a Google account. While we can use R on Google Colab, it is designed for Python. Advantages over R Studio Cloud include the ability to use GPUs, not just CPUs.  -->

<!-- To get started, while logged into Google, go to [Colab](colab.research.google.com) and select 'New notebook'. -->

<!-- To get started you need to tell Google Colab that you want to use R. You can do this by using this: https://colab.research.google.com/notebook#create=true&language=r. -->

<!-- At this point you have a Jupyter notebook open that will run R. (But it is not a R Markdown document.) You can install packages as normal, e.g. `install.packages("tidyverse")`, and then call the package e.g. `library(tidyverse)`. -->

<!-- Google Colab is a good option if you have a good reason for using the broader capabilities that it has. If you want to go deeper into that then the Morris reading has a bunch of options that you can explore, but as Morris puts it 'Colab is a gateway drug - for large-scale processing pipelines you'll need to move up to Google Cloud Platform or one of its competitors AWS, Azure, etc.' and that is what we will do now. -->

Amazon Web Services is a cloud service from Amazon. To get started we need to create an AWS Developer account [here](https://aws.amazon.com/developer/) (Figure \@ref(fig:awsone)).

<div class="figure" style="text-align: center">
<img src="figures/aws_one.png" alt="AWS Developer website" width="95%" />
<p class="caption">(\#fig:awsone)AWS Developer website</p>
</div>

After we have created an account, we need to select a region where the computer that we will access is located. After this, we want to "Launch a virtual machine" with EC2 (Figure \@ref(fig:awstwo)).

<div class="figure" style="text-align: center">
<img src="figures/aws_two.png" alt="AWS Developer console" width="95%" />
<p class="caption">(\#fig:awstwo)AWS Developer console</p>
</div>

The first step is to choose an Amazon Machine Image (AMI). This provides the details of the computer that you will be using. For instance, a local computer may be a MacBook running Monterey. Louis Aslett provides AMIs that are already set-up with R Studio and much else [here](http://www.louisaslett.com/RStudio_AMI/). We can either search for the AMI of the region that we registered for, or click on the relevant link on Aslett's website. For instance, to use the AMI set-up for the Canadian central region we search for 'ami-0bdd24fd36f07b638'. The benefit of using these AMIs is that they are set-up specifically for R Studio, but the trade-off is that they are a little outdated, as they were compiled in August 2020.



In the next step we can choose how powerful the computer will be. The free tier is basic computer, but we can choose better ones when we need them. At this point we can pretty much just launch the instance (Figure \@ref(fig:awsthree)). If we start using AWS more seriously we could go back and select different options, especially around the security of the account. AWS relies on key pairs. And so we will need to create a PEM and save it locally (Figure \@ref(fig:awsfive)). We can then launch the instance.


<div class="figure" style="text-align: center">
<img src="figures/aws_three.png" alt="AWS Developer launch instance" width="95%" />
<p class="caption">(\#fig:awsthree)AWS Developer launch instance</p>
</div>

<div class="figure" style="text-align: center">
<img src="figures/aws_five.png" alt="AWS Developer establishing a key-pair" width="95%" />
<p class="caption">(\#fig:awsfive)AWS Developer establishing a key-pair</p>
</div>

After a few minutes, the instance will be running. We can use it by pasting the 'public DNS' into a browser. The username is 'rstudio' and the password is the instance ID.

We should have R Studio running, which is exciting. The first thing to do is probably to change the default password using the instructions in the instance.

We do not need to install, say, `tidyverse`, instead we can just call the library and keep going. This is because this AMI comes with many packages already installed. We can see the list of packages that are installed with `installed.packages()`. For instance, `rstan` is already installed, and we could set-up an instance with GPUs if we needed.

Perhaps as important as being able to start an AWS instance is being able to stop it (so that we do not get billed). The free tier is pretty great, but we do need to turn it off. To stop an instance, in the AWS instances page, select it, then 'Actions -> Instance State -> Terminate'.






<!-- ## R packages -->

<!-- To this point we have largely been using R Packages to do things for us. However, another way is to have them loaded -->

<!-- DoSS Toolkit -->


<!-- ## Shiny -->



## Plumber and model APIs

The general idea behind the `plumber` package [@plumber] is that we can train a model and make it available via an API that we can call when we want a forecast. It is pretty great.

Just to get something working, let us make a function that returns 'Hello Toronto' regardless of the output. Open a new R file, add the following, and then save it as 'plumber.R' (you may need to install the `plumber` package if you've not done that yet).


```r
library(plumber)

#* @get /print_toronto
print_toronto <- function() {
  result <- "Hello Toronto"
  return(result)
}
```

After that is saved, in the top right of the editor you should get a button to 'Run API'. Click that, and your API should load. It will be a 'Swagger' application, which provides a GUI around our API. Expand the GET method, and then click 'Try it out' and 'Execute'. In the response body, you should get 'Toronto'. 

To more closely reflect the fact that this is an API designed for computers, you can copy/paste the 'request HTML' into a browser and it should return 'Hello Toronto'.


### Local model

Now, we are going to update the API so that it serves a model output, given some input. We are going to follow @buhrplumber fairly closely.

At this point, we should start a new R Project. To get started, let us simulate some data and then train a model on it. In this case we are interested in forecasting how long a baby may sleep overnight, given we know how long they slept during their afternoon nap.


```r
library(tidyverse)
set.seed(853)

number_of_observations <- 1000

baby_sleep <- 
  tibble(afternoon_nap_length = rnorm(number_of_observations, 120, 5) %>% abs(),
         noise = rnorm(number_of_observations, 0, 120),
         night_sleep_length = afternoon_nap_length * 4 + noise,
         )

baby_sleep %>% 
  ggplot(aes(x = afternoon_nap_length, y = night_sleep_length)) +
  geom_point(alpha = 0.5) +
  labs(x = "Baby's afternoon nap length (minutes)",
       y = "Baby's overnight sleep length (minutes)") +
  theme_classic()
```

Let us now use `tidymodels` to quickly make a dodgy model.


```r
set.seed(853)
library(tidymodels)

baby_sleep_split <- rsample::initial_split(baby_sleep, prop = 0.80)
baby_sleep_train <- rsample::training(baby_sleep_split)
baby_sleep_test <- rsample::testing(baby_sleep_split)

model <- 
  parsnip::linear_reg() %>%
  parsnip::set_engine(engine = "lm") %>% 
  parsnip::fit(night_sleep_length ~ afternoon_nap_length, 
               data = baby_sleep_train
               )

write_rds(x = model, file = "baby_sleep.rds")
```

At this point, we have a model. One difference from what you might be used to is that we have saved the model as an '.rds' file. We are going to read that in.

Now that we have our model we want to put that into a file that we will use the API to access, again called 'plumber.R'. And we also want a file that sets up the API, called 'server.R'. So make an R script called 'server.R' and add the following content:


```r
library(plumber)

serve_model <- plumb("plumber.R")
serve_model$run(port = 8000)
```

Then in 'plumber.R' add the following content:


```r
library(plumber)
library(tidyverse)

model <- readRDS("baby_sleep.rds")

version_number <- "0.0.1"

variables <- 
  list(
    afternoon_nap_length = "A value in minutes, likely between 0 and 240.",
    night_sleep_length = "A forecast, in minutes, likely between 0 and 1000."
  )

#* @param afternoon_nap_length
#* @get /survival
predict_sleep <- function(afternoon_nap_length=0) {
  afternoon_nap_length = as.integer(afternoon_nap_length)
  
  payload <- data.frame(afternoon_nap_length=afternoon_nap_length)
  
  prediction <- predict(model, payload)

  result <- list(
    input = list(payload),
    response = list("estimated_night_sleep" = prediction),
    status = 200,
    model_version = version_number)

  return(result)
}
```

Again, after we save the 'plumber.R' file we should have an option to 'Run API'. Click that and you can try out the API locally in the same way as before.


### Cloud model

To this point, we have got an API working on our own machine, but what we really want to do is to get it working on a computer such that the API can be accessed by anyone. To do this we are going to use [DigitalOcean](https://www.digitalocean.com). It is a charged service, but when you create an account, it will come with $100 in credit, which will be enough to get started.

This set-up process will take some time, but we only need to do it once. Install two additional packages that will assist here are `plumberDeploy` [@plumberdeploy] and `analogsea` [@citeanalogsea].


```r
install.packages("plumberDeploy")
remotes::install_github("sckott/analogsea")
```

Now we need to connect the local computer with the DigitalOcean account. 


```r
analogsea::account()
```

Now we need to authenticate the connection, and this is done using a SSH public key.


```r
analogsea::key_create()
```

What you want is to have a '.pub' file on our computer. Then copy the public key aspect in that file, and add it to the SSH keys section in the account security settings. When we have the key on our local computer, then we can check this.


```r
ssh::ssh_key_info()
```

Again, this will all take a while to validate. DigitalOcean calls every computer that we start a 'droplet'. So if we start three computers, then we will have started three droplets. We can check the droplets that are running.
 

```r
analogsea::droplets()
```

If everything is set-up properly, then this will print the information about all droplets that you have associated with the account (which at this point, is probably none). We first create a droplet.


```r
id <- plumberDeploy::do_provision(example = FALSE)
```

Then we get asked for the SSH passphrase and then it will just set-up a bunch of things. After this we are going to need to install a whole bunch of things onto our droplet.


```r
analogsea::install_r_package(droplet = id, c("plumber", 
                                             "remotes", 
                                             "here"))
analogsea::debian_apt_get_install(id, "libssl-dev", 
                                  "libsodium-dev", 
                                  "libcurl4-openssl-dev")
analogsea::debian_apt_get_install(id, 
                                  "libxml2-dev")

analogsea::install_r_package(id, c("config",
                                   "httr",
                                   "urltools",
                                   "plumber"))

analogsea::install_r_package(id, c("xml2"))
analogsea::install_r_package(id, c("tidyverse"))

analogsea::install_r_package(id, c("tidymodels"))

```

And then when that is finally set-up (it will take 30 minutes or so) we can deploy our API.


```r
plumberDeploy::do_deploy_api(droplet = id, 
                             path = "example", 
                             localPath = getwd(), 
                             port = 8000, 
                             docs = TRUE, 
                             overwrite=TRUE)
```






## Exercises and tutorial

### Exercises

### Tutorial



