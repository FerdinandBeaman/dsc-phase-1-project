# Microsoft Movie Maker Project
By Ferdinand Beaman
* Student pace: part time
* Scheduled project review date: May 3rd, 2023
* Instructor name: Mark Barbour
* Blog post URL: TBD

## Project Goal

This project is here to inform Microsoft of what factors will help their first (hypothetical) movie be a success. And by "success", I mean "generate the most profits".

### Data Source and Exploration
The data I used came primarily from [imdb.com](https://www.imdb.com/) and [the-numbers.com](https://www.the-numbers.com/). These websites have information about:
* titles, both domestic and international
* release dates
* cast and crew
* budgets
* Ticket sales, both domestic and international

Since my goal is to find what movies are profitable and not what movies are well-reviewed, I'm ignoring the ratings-related files.

# Merging all the data

Everything we need is spread out amongst a few different dataframes. So we're going to stick them all together and then cut out what we don't need. 

There are three general categories of information I want to look at: the finances, the genre, and who worked on it. Lastly, we should also stick with modern movies... whatever that means.


## Lining the numbers up

The data from "the-numbers" needs a little cleaning to turn it into something useful. But it has all the financial data that we're going to using as our measure of "success".

Now to get the first number I really want: profits! (This will be the difference between worldwide gross and budget)

Awful lot of Marvel and other Disney products on there. Practically half of the top 15.

Now there's no easy way to parse how much of that has to do with Marvel's branding or how much of it has to do with Marvel's quality. But it's in the dataset nonetheless.

## Getting a sense of style

I bet that most people's first answer to "What kind of movie should you make?" is a genre. So lets get those analyzed.

How are the genres labeled?

It turns out that each entry is a list, but each list has only one element which is just a *single string* with all of the genres written down all at once. Or it is NoneType object (like the penultimate entry above). They will each require attention to handle properly.

We're going to have to make each genre into its own column if we're going to get anywhere.

Mwah! Just to orient myself, let's see what the most common genres are.

Wow! There was no way that I would have guessed that documentaries would be king, but I understand in retrospect.

## Asking for Direction
In my experience, a director makes or breaks a movie as much as any actor, maybe even moreso.

For fun, I decided to see who are the most common directors.

Well that's odd, maybe they directed a lot of foreign films...
*Checks Google*
...Nope! Omer Pasha directs music videos.

I'll have to make sure my finalists are movie directors in particular.

Come to think of it, I'm surprised to not see Speilberg in the top 10. What does the database say?

*NINE?* 
It was here that I had thought I did something very wrong. But, thankfully, it turns out that the IMDB data is only from 2010 forward.<br> Phew.

I suppose that's it for this step. Next, I'll join them all together before cutting out the smaller and older films.

# Finalizing the dataset

## Stitching it together
First, I think it would be easy to sew the director table onto "movie basics" since they share an obvious column: movie_id.

## Cutting the chaff
All of the movies I want are going to be less than 10 years old. However, I'm going to have to remove all the entries from 2020 and 2021 due to the pandemic.

Pre-pandemic, the average movie released in theaters made 12,487,209 in the US, so I think it'll be a fair starting point to say that in order for a movie to be "relevant" to my project, it has to have made over half of that.

There are actually a lot of duplicates in this dataset. Why? Because movies with multiple directors are showing up as multiple entries.

I can foresee this being useful, so we'll keep this dataset with multiple directors as well as one where the duplications are cut out.

Good.

# Measurements

## Picking the Medium
This part should be straightforward. Animation or Live Action?

![animation_v_live.png](./images/animation_v_live.png)

Well that's not even close! Animated movies are almost three times as profitable by mean, and nearly *quintuple* be median! One suggestion down, two to go.

Just how common are animated movies, anyway?

Okay, so that's a fair enough sample.

## Picking the Director

I'll get a look at the most profitable directors by both mean and median, then choose from among those the ones with the largest catalogs.

Clearly there's a bunch of overlap, and I am going to take just the directors whose names appear in both lists.

Everyone was in both lists. Unexpected. That probably means a lot of people only have 1 qualified movie to their name.

There really doesn't seem to be that big of a difference the further down the list we go. Surprisingly, the Russos (of Avengers: Endgame fame) fall out of the top 10 using the median.

How many movies these directors have made?

Ah, so the reason why the median scores are what they are is because so many of these filmmakers have only one qualifying flick. Even with this many candidates, only the Russos stand out with three relevant movies in the last 10 years. Even though they fell out of the top 10 by median, they were still able to even qualify for this list in the first place despite their second and third place movies being less impressive.

As for the other directors who had multiple films that qualified:<br>
James Wan directed The Conjuring and Aquaman<br>
Kyle Balda directed two of the correctly-maligned Minions movies<br>
and Pierre Coffin... also directed two Minions movies.

Colin Treverrow was the leader on both lists with one movie. Luckily for us, that film *was* both an Adventure and Sci-Fi movie, making him a very defensible choice.

All in all, I'd still give it to the Russo Brothers, because they've done it more consistently. But it's probably debatable. It may be impossible to know how much of their success just has to do with the momentum Marvel supplies just by brand recognition.

![directors.png](./images/directors.png)

## Picking the genre
I'm going to make a dataframe that's just made up of the profits (mean and median) for each genre.

Now we isolate the sorted data for the profit columns.

Musicals take the gold medal?
Well, with only 2 representatives, I think it's fair to say that it's not exactly a tried and true formula for success. 

So, we'll take a closer look at the silver and bronze finalists instead: Sci-Fi and Adventure.

We can first make sure that outliers aren't driving the data, and we can also see if these genres are buoyed by data from the early 2010s.

While a little over 20% of our sample of Sci-Fi and Adventure movies lose money, it seems like many of the genres share this fate. And this boxplot has its outliers filtered out, so the big blockbusters are not solely responsible for these two pulling ahead.

Seems good to me. Let's just graph the overall means and medians now.

![genres_over_time.png](./images/genres_over_time.png)
![genres_inc_music.png](./images/genres_inc_music.png)

# So what do we conclude?
Putting it all together, I'm actually very pleased with the results.

Action and comedy are "ok", but I think that it would be wise to separate this project from a Marvel style movie. I'd suggest focusing on the two core genres to further make this film distinct from the competition.

So Microsoft could set itself apart with an *Animated Sci-Fi Adventure directed by the Russo Brothers*, perhaps with a more serious edge. If they turn it down, get Colin Treverrow. Failing that, James Wan will do.

I'd watch that.

# Repository Structure

├── CONTRIBUTING.md
├── LICENSE.md
├── im.db
├── /images
├── movie_data_erd.jpeg
├── zippedData
├── README.md
├── presentation.pdf
└── Ferdinand Beaman Phase 1 Project.ipynb