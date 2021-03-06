---
layout: post
title: Milestone 1
---

# Question 1: Warm-up

## 1
[
* which is the ratio of their shots saved over the total number of shots they faced
* What issues do you notice by using this metric to rank goalies?
* What could be done to deal with this?

]

## 2

[Filter out the goalies using your proposed approach above, and produce a bar plot with player names on the y-axis and save percentage (‘SV%’) on the x-axis]

## 3

[Discuss what other features could potentially be useful in determining a goalie’s performance]

# Question 2: Data Acquisition

There are two important functions situated in the ift6758.data module that are used to download our dataset:

![image](/images/load_entire_dataset.png)
![image](/images/import_dataset.png)

The function `load_entire_dataset` lets us load the regular season and playoff data for every season since 2016, while `import_dataset` encapsulates our fetching behaviour for a given season and a type (regular/playoff). The `import_dataset` function works by looking for an existing dataset and returning it as a json object if it exists, otherwise it fetches all the games in a given season according to that season's schedule, saves the result in a json file, then returns the data as a json object. As such, our dataset is composed of two json files per season: one for the regular season and one for the playoffs.

To download the dataset, all we have to do is to execute the following in a notebook cell:

```
from ift6758.data import load_entire_dataset
load_entire_dataset()
```

This will download the dataset into the data module under the `dataset` directory, unless a path is given to `import_dataset` within the function definition.

Then to access a given season's data we simply need to call "import_dataset". For example, here is the code to load the raw json data for the 2016-2017 season:

```
from ift6758.data import import_dataset
2016_regular_json_data = import_dataset(2016, "R", returnData=True)
```

To have a dataframe of every season's data, one needs to extract (and tidy) every season as shown above, then store all the resulting data in a common dataframe.


# Question 3: Interactive Debugging Tool


![image](/images/Interactive_debugging_tool_screenshot.PNG)

Here is a screenshot showing the tool for question 3.
It is built with 3 nested slider widgets to control which event is display.
A portion of the event JSON is displayed as well as its position on the rink.
One slider controls the dataset/season, another controls which game and the third controls which event from that game is displayed.

# Question 4: Tidy Data

## 1
[a small snippet of your final dataframe (e.g. using head(10)). You can just include a screenshot rather than fighting to get the tables neatly formatted in HTML/markdown.]

## 2
[Discuss how you could add the actual strength information (i.e. 5 on 4, etc.) to both shots and goals, given the other event types (beyond just shots and goals) and features available.]

## 3
[In a few sentences, discuss some additional features you could consider creating from the data available in this dataset.]

# Question 5: Simple Visualizations

## 1
[
* histogram of shot types over all teams in a season of your choosing.
* Overlay the number of goals overtop the number of shots.
* What appears to be the most dangerous type of shot?
* The most common type of shot?

]

## 2
[
* What is the relationship between the distance a shot was taken and the chance it was a goal?
* Produce a figure for each season between 2018-19 to 2020-21 to answer this
* a couple of sentences describing your figure
* Has there been much change over the past three seasons

]

## 3
[
* Combine the information from the previous sections to produce a figure that shows the goal percentage (# goals / # shots) as a function of both distance from the net, and the category of shot types (you can pick a single season of your choice)
* Briefly discuss your findings

]

# Question 6: Advanced Visualizations: Shot Maps

## 1

{% include shot-heatmap.html%}

## 2

The above heat map shows the difference in frequence between a team's shots and a league average for a given season. Data is shown only in the "offensive" zone where the middle of the rink is the y-axis, and the distance from the goal is the x-axis. 

The contour plot represents the difference in rate of shots per hour, where a denser region represents a more frequent shot location for a given team compared to that year's average. Conversly, a team that has shot less than the league's average that year will be represented by blue contours.

The contours have been smoothed to encompass a "better defined" region, thus for small differences in rates of shot we are presented with an either pale red or pale blue contour that are functionally equivalent to 0. However, for presentation purposes we decided to keep all the information available to us on the chart as we can hover over the figure to see the difference in rates of shot, shown as the "z" axis.

## 3

### Colorado Avalanche 2016-2017 shot map:
![image](/images/colorado2016.png)

### Colorado Avalanche 2020-2021 shot map:
![image](/images/colorado2020.png)

We can see from the 2016 season shot map that the Colorado Avalanche really struggled to control the puck in the enemy's defensive zone. Notice that they shot mostly from the middle left area of the rink, and often shot from either behind the goal or in the back (close from the center) of the offensive zone. They also shot much less in front of the goal than that year's league average, which most likely hurt their standing that year since that's the most dangerous shot area.

The 2020-2021 season shot map tells a diffrent story: that year, the Avalanche seemed to shoot more often than that year's average all around the offensive zone. Mainly, they shot more often in front of the net, in the center of the offensive zone, and closer to the net from the sides.  This appears to show they had a much stronger offense that season. 

The results make sense considering the Avalanche was the last team in their division in the 2016-2017 season, whereas the Avalanche are the number one team in their division (and the league) for the 2020-2021 season. As we know, the stronger the offense, the more goals are scored, which increases the team's overall standing.

## 4

### Buffalo 2018-2019 shot map:
![image](/images/buffalo2018.png)

### Buffalo 2019-2020 shot map:
![image](/images/buffalo2019.png)

### Buffalo 2020-2021 shot map:
![image](/images/buffalo2020.png)

### Lightning 2018-2019 shot map:
![image](/images/lightning2018.png)

### Lightning 2019-2020 shot map:
![image](/images/lightning2019.png)

### Lightning 2020-2021 shot map:
![image](/images/lightning2020.png)

We can make two main observations from the above shotmaps: the Buffalo really seems to really struggle offensively, while the Lightning possess a very strong offense. 

Notice how most of the Buffalo's shots come from the sides of the offensive zone while very few are directly in front of the net. More shots than average also seem to come from behind the net, which most likely show that their offense had to get rid of the puck as they could not maneuver it within a good shot location. Overall the Buffalo's offense seem to be more scattered over the offensive zone and most shots are shot in less dangerous areas, resulting in less goals overall, which could explain the Buffalo's poor performance over the past few years.

Almost inversely, the Lightning's shot areas are mainly concentrated in front of the net and mostly in the center of the offensive zone. Interestingly, the Lightning's most frequent shot area (in front of the net) is slightly behind the usual "front of the net" area observed for the league's average. As this has been the case for 3 consecutive years, it seems like that area plays into their strategy. The Lightning shooting more often from the center zone could also explain the team's high standing; they probably have much more control over the puck in the offensive zone, and they can effectively shoot from more dangerous areas, yielding more goals.

Those heat maps are pretty useful, to reason about a team's offensive performance in terms of shot location and frequency. However, they do not tell the whole story. For instance, a seemingly frequent shot area for a team (e.g. in front of the net) compared to the average does not indicate an absolute increase in performance. The fact that certain zones are more "dangerous" than others plays part when assessing a team's performance but it does not tell us whether that area was definitvely the reason (or not) why a team did well or not. For instance, in the 2017-2018 season the Canadiens had an above average rate of shot right in front of the net, but the team still ended up being in the bottom of the standing. To get the full picture of a team's performance, we would need to aggregate more performance metrics and compare all of them between teams for a given season.