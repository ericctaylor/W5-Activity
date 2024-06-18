# W5-Activity

---
title: "W5 Activity"
author: "Eric Carrieri Taylor"
date: "2024-06-18"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

### Voter Registration by Month
###### The histogram below shows the total number of new voter registrations for each month, aggregated across all years. This visualization helps identify which months have higher or lower voter registration activity, providing insights into seasonal trends in voter registration.

```{r}
library(ggplot2)

data <- read.csv("/Users/erictaylor/Downloads/New Voter Registration.csv")

data$Month <- match(data$Month, month.abb)

if (any(is.na(data$Month))) {
  stop("There are unmatched month values in the data.")
}

monthly_registration <- aggregate(data$New.registered.voters, by = list(Month = data$Month), sum)
colnames(monthly_registration) <- c("Month", "NewRegisteredVoters")

ggplot(monthly_registration, aes(x = factor(Month, levels = 1:12, labels = month.abb), y = NewRegisteredVoters)) +
  geom_col(fill = "skyblue", color = "black") +
  labs(title = "Voter Registration by Month", x = "Month", y = "Number of New Registered Voters") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

### Voter Registration by State and Month
###### The scatter plot below shows the number of new voter registrations by state and month. Each point represents the number of new registrations for a specific state and month, allowing for a comparison of registration activity across different states and times of the year.

```{r}
state_month_registration <- aggregate(data$New.registered.voters, by = list(State = data$Jurisdiction, Month = data$Month), sum)
colnames(state_month_registration) <- c("State", "Month", "NewRegisteredVoters")

ggplot(state_month_registration, aes(x = factor(Month, levels = 1:12, labels = month.abb), y = NewRegisteredVoters, color = State)) +
  geom_point() +
  labs(title = "Voter Registration by State and Month", x = "Month", y = "Number of New Registered Voters") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```
