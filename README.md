# TIL
Today I Learned, literally

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

