

install.packages("readr")
install.packages("dplyr")
install.packages("tidytext")
install.packages("tm")
install.packages("wordcloud")
install.packages("ggplot2")
install.packages("RColorBrewer")
install.packages("readxl")


# Loading necessary libraries
library(readr)
library(dplyr)
library(tidytext)
library(tm)
library(wordcloud)
library(ggplot2)
library(readxl)

# Loading the datasets
wrlddata <- read_excel("C:/Users/Albin/Documents/GitHub/Covid-19-tweet-analysis/Covid Data1.xlsx")

tweets= read_csv("C:/Users/Albin/Documents/GitHub/Covid-19-tweet-analysis/Covid-19 Twitter Dataset (Apr-Jun 2020).csv")

print(head(tweets))

tweets$cleaned_tweet <- sapply(tweets$original_text, clean_tweet)

print(colnames(tweets))

tweets_words <- tweets %>%
  unnest_tokens(word, cleaned_tweet)

# Removing stopwords
data("stop_words")
tweets_words <- tweets_words %>%
  anti_join(stop_words, by = "word")

custom_stopwords <- c("covid", "amp")
tweets_words <- tweets_words %>%
  filter(!word %in% custom_stopwords)

# Create a word frequency table
word_freq <- tweets_words %>%
  count(word, sort = TRUE)

# Generate the word cloud
set.seed(1234)
wordcloud(words = word_freq$word, 
          freq = word_freq$n, 
          min.freq = 1,
          max.words = 100,
          random.order = FALSE,
          rot.per = 0.35,
          colors = brewer.pal(8, "Dark2"))

# Optionally, save the word cloud as an image
png("wordcloud.png", width = 800, height = 600)
wordcloud(words = word_freq$word, 
          freq = word_freq$n, 
          min.freq = 1,
          max.words = 100,
          random.order = FALSE,
          rot.per = 0.35,
          colors = brewer.pal(8, "Dark2"))
dev.off()

