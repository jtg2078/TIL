# TIL
Today I Learned, literally

## 5-6

High-intensity interval training (HIIT), is great!

* Short bursts of just a few minutes of exhausting physical activity can prepare muscles to work harder, boosting the production of new mitochondria [link](http://www.thelatestnews.com/scientists-discovered-why-can-high-intensity-interval-training-match-endurance-training/)
* It seems like the "best" approach is to do low intensity cardio training regularly, and high intensity interval training one to two days a week [link](https://www.reddit.com/r/Fitness/comments/3rmp9a/researchers_discovered_why_a_few_minutes_of_high/)
* One HIIT, One tempo(which is like a moderate high intensity non interval for like 20 minutes) , One Long run(slow and long), in between are easy

How Long and Intense Your Low-Intensity Intervals Should Be

> Start out with a 1:2 ratio between high- and low-intensity intervals. For example, 1 minute at high-intensity and 2 minutes at low.
As you get fitter, you can work toward a 1:1 ratio.
Your rest periods should also be active recovery, where you keep moving, not a standstill.
Studies have shown that active, not passive, recovery is advantageous for reaching Vmax during the high-intensity periods and eliciting the adaptive response to the exercise that we’re after.

How Long Should Your HIIT Workouts Be?

> The great thing about HIIT is how much you get out of relatively small amounts of it. That said, it can be quite stressful on the body, which means you don’t want to overdo it.
Start your workouts with 2 to 3 minutes of low-intensity warm-up and then do 20 to 25 minutes of intervals followed by 2 to 3 minutes of warm-down and you’re done.
There’s just no need to do more than this in each workout.

[link](https://www.reddit.com/r/Fitness/comments/3rsl22/what_is_the_best_hiit_workout_for_a_beginner/) [link2](https://www.reddit.com/r/Fitness/comments/3vkepf/what_is_your_hiit_sprint_routine/)

[THE ULTIMATE 8-WEEK HIIT FOR FAT-BURNING PROGRAM](http://www.bodybuilding.com/fun/ultimate-8-week-hiit-for-fat-burning-program.html)

* all cap so it must be really ultimate

Quick syntax lookup for various programming languages

* [Programming cheat sheets (overapi.com)](http://overapi.com/)
* [Learn X in Y minutes](https://learnxinyminutes.com/)

## 5-5

[how to broadcast with two computers](http://help.twitch.tv/customer/portal/articles/1988680-broadcasting-with-two-computers)

* one gaming pc and one streaming pc
* streaming pc uses capture card, links up with gaming pc via HDMI, duplicate monitor mode on gaming pc
* use [Audio Repeater](http://software.muzychenko.net/eng/vac.htm) to duplicate game audio and sends to capture card via hdmi
* [OBS](https://obsproject.com/) for creating streaming source  

## 5-4
iOS native video player does not support .srt subtitle, only .scc subtitle is supported  

* Scenarist Closed Caption (.scc file extension)
* [srt file format](https://en.wikipedia.org/wiki/SubRip)

SRT file format is generally consist of following unit(s)

```
15
00:03:03,643 --> 00:03:05,186
I can always...
```

* `15` is the sequence number
* `00:03:03,643 --> 00:03:05,186` is the timestamp and duration
* `I can always...` is the content of the subtitle

It possible that the sequence number and timestamp don't match... e.g. the sequence number is small but its timestamp is much later. so when this happen the video player might not show any subtitle when it encounter this kind of discrepancy.

So how do we fix this?

* we can use the rule -> timestamp dictates its sequence number
* use subtitle editing app [Jubler](http://www.jubler.org/) to sort subtitle units based on timestamp, and regenerate sequence number




