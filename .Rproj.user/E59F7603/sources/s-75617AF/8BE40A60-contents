

## 5- load
#install.packages("rtweet")
##devtools::install_github("mkearney/rtweet")
library(rtweet)


## 8- view rtweet's authorization vignette
vignette("auth", package = "rtweet")
## name of twitter app
app_name <- "mwk_twitter_app"


## 12- copy and pasted keys
consumer_key <- "XYznzPFOFZR2a39FwWKN1Jp41"
consumer_secret <- "CtkGEWmSevZqJuKl6HHrBxbCybxI1xGLqrD5ynPd9jG0SoHZbD"


## 13- create token
token <- create_token(app_name, consumer_key, consumer_secret)
token


## 14- save token to home directory
path_to_token <- file.path(path.expand("~"), ".twitter_token.rds")
saveRDS(token, path_to_token)
## create env variable TWITTER_PAT (with path to saved token)
env_var <- paste0("TWITTER_PAT=", path_to_token)
## save as .Renviron file (or append if the file already exists)
cat(env_var, file = file.path(path.expand("~"), ".Renviron"),
  fill = TRUE, append = TRUE)


## 15- refresh .Renviron variables
readRenviron("~/.Renviron")


## 18- get status IDs of jack's friend's
fds <- get_friends("jack")
## get friends of multiple accounts
fds <- get_friends(c("hadleywickham", "NateSilver538", "Nate_Cohn"))
fds


## 19- get mike's followers
kmw <- get_followers("kearneymw")
kmw
## get all of trump's followers
#rdt <- get_followers("realdonaldtrump", n = 5e7, retryonratelimit = TRUE)


## 21- search for a keyword
rt <- search_tweets(q = "rstats")
## search for a phrase
rt <- search_tweets(q = "data science")
## search for multiple keywords
rt <- search_tweets(q = "rstats AND python")
## search tweets (q = search query; n = desired number of tweets to return)
rt <- search_tweets(q = "rstats", n = 1000)


## 22- search for any mention of a list of words
rt <- search_tweets("statistics OR statistical OR quantitative")
## search for tweets in english that are not retweets
rt <- search_tweets("rstats", lang = "en", include_rts = FALSE)
## search for tweets in english that are not retweets
rt <- search_tweets("lang:en", geocode = lookup_coords("Chicago, IL"))


## 23- search for english tweets sent via ifttt
rt <- search_tweets("lang: source:ifttt")
table(rt$source)


## 25- get tweets from CNN timeline
cnn <- get_timeline("cnn", n = 3200)
ts_plot(cnn, "hours")


## 26- get mike's favorites
kmw_favs <- get_favorites("kearneymw", n = 3000)
ts_plot(kmw_favs, "3 days")


## 28- lookup status IDs
status_ids <- c("947235015343202304", "947592785519173637",
  "948359545767841792", "832945737625387008")
twt <- lookup_tweets(status_ids)


## 29- lookup user (screen  names)
users <- c("hadleywickham", "NateSilver538", "Nate_Cohn")
usr <- lookup_users(users)


## 31- random sample
st1 <- stream_tweets(q = "", timeout = 30)
## keyword filter
st2 <- stream_tweets(q = "realDonaldTrump,Mueller", timeout = 30)
## bounding box
st3 <- stream_tweets(q = lookup_coords("London, GB"), timeout = 30)


## 36- (NETWORK ANALYSIS) get friends of multiple accounts
fds <- get_friends(c("hadleywickham", "NateSilver538", "Nate_Cohn"))
## frequency count of accounts followed by the users queried above
tbl <- table(fds$user_id)
## subset fds data to only those followed by 3 or more
fds3 <- subset(fds, user_id %in% names(tbl[tbl > 2L]))
## convert fds3 to matrix
mat <- as.matrix(fds3)
## convert to graph object
mat <- igraph::graph_from_edgelist(mat)
## plot network
plot(mat)


## 38- Firehose for free
## vector of all supported language abbreviations
langs <- c("en", "ar", "bn", "cs", "da", "de", "el", "es", "fa", "fi", "fil",
"fr", "he", "hi", "hu", "id", "it", "ja", "ko", "msa", "nl", "no", "pl",
"pt", "ro", "ru", "sv", "th", "tr", "uk", "ur", "vi", "zh-cn", "zh-tw")
## add param name (lang) to each
langs <- paste0("lang:", langs)
## collapse into single OR search
langs <- paste(langs, collapse = " OR ")
## search for most recent 6,000 tweets in any language
rt <- search_tweets(langs, n = 6000)
