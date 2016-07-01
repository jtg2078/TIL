# TIL
Today I Learned, literally

## 7-1

iOS stuff

* [How do I convert an NSString value to NSData?](http://stackoverflow.com/questions/901357/how-do-i-convert-an-nsstring-value-to-nsdata)
* [Is it possible to force Excel recognize UTF-8 CSV files automatically?](http://stackoverflow.com/questions/6002256/is-it-possible-to-force-excel-recognize-utf-8-csv-files-automatically)
* [為何使用 Microsoft Excel 打開匯出的報名人 CSV 檔案是亂碼？](http://support.kktix.com/knowledgebase/articles/278363-%E7%82%BA%E4%BD%95%E4%BD%BF%E7%94%A8-microsoft-excel-%E6%89%93%E9%96%8B%E5%8C%AF%E5%87%BA%E7%9A%84%E5%A0%B1%E5%90%8D%E4%BA%BA-csv-%E6%AA%94%E6%A1%88%E6%98%AF%E4%BA%82%E7%A2%BC)

[Mousewheel horizontal scrolling](http://stackoverflow.com/questions/25228158/mousewheel-horizontal-scrolling)

```
$(function() {
        $("html, body").mousewheel(function(event, delta) {
            this.scrollLeft -= (delta * 30);
            event.preventDefault();
        });
    });
```


## 6-27

[How to get the date without Time from NSDate?](http://stackoverflow.com/questions/11117324/how-to-get-the-date-without-time-from-nsdate)

```
NSDateComponents *components = [[NSCalendar currentCalendar] 
             components:NSYearCalendarUnit|NSMonthCalendarUnit|NSDayCalendarUnit 
              fromDate:[NSDate date]];
NSDate *startDate = [[NSCalendar currentCalendar] 
             dateFromComponents:components];
```

## 6-23

[How to lose margin/padding in UITextView?](http://stackoverflow.com/questions/746670/how-to-lose-margin-padding-in-uitextview)

```
self.textView.textContainer.lineFragmentPadding = 0;
self.textView.textContainerInset = UIEdgeInsetsZero;
```

## 6-08

links

* [Common Mistakes With Adding Custom Fonts to Your iOS App](http://codewithchris.com/common-mistakes-with-adding-custom-fonts-to-your-ios-app/)
* [Custom Fonts in Swift](https://grokswift.com/custom-fonts/)
* [How to integrate and use Font Awesome with Objective-C or Swift in an Xcode project?](http://stackoverflow.com/questions/10569878/how-to-integrate-and-use-font-awesome-with-objective-c-or-swift-in-an-xcode-proj)
* [Custom UIView from Xib file in Xcode 5 for Reusable Components - Part 1](https://www.youtube.com/watch?v=xP7YvdlnHfA)
* [Create an IBDesignable UIView subclass with code from an XIB file in Xcode 6](http://supereasyapps.com/blog/2014/12/15/create-an-ibdesignable-uiview-subclass-with-code-from-an-xib-file-in-xcode-6)

## 5-26

links

* [Identify if the navigation is a pop or a push in a child view controller](http://stackoverflow.com/questions/31959245/identify-if-the-navigation-is-a-pop-or-a-push-in-a-child-view-controller)

```
- (void)viewWillDisappear:(BOOL)animated
{
    [super viewWillDisappear:animated];
    
    if(self.isMovingFromParentViewController == YES && self.isDirty)
    {
        // do stuff...
    }
}
```

* 

## 5-25

###how to save image to photo library in iOS

__use `UIImageWriteToSavedPhotosAlbum` function__

```
- (void)saveImageToPhotoAlbum:(UIImage *)image
{
    id contextInfo = @"can be anything";
    
    UIImageWriteToSavedPhotosAlbum(image,
                                   self,
                                   @selector(image:didFinishSavingWithError:contextInfo:),
                                   (__bridge_retained  void *)(contextInfo));
}

- (void)image:(UIImage *)image didFinishSavingWithError:(NSError *)error contextInfo:(void *)contextInfo
{
    id myInfo = (__bridge_transfer id)contextInfo;
    // use error to check success or not
    // contextInfo is watever you pass in
}
```

but this way you can't get the path of the image you just saved


__use `ALAssetsLibrary`__


```
- (void)saveImageToPhotoAlbum2:(UIImage *)image
{
    ALAssetsLibrary *library = [[ALAssetsLibrary alloc] init];
    
    [library writeImageToSavedPhotosAlbum:image.CGImage
                              orientation:(ALAssetOrientation)image.imageOrientation
                          completionBlock:^(NSURL *assetURL, NSError *error) {
        
        // now you can use assetURL to find the save image's url
        
    }];
    
}
```

but `ALAssetsLibrary` is deprecated in iOS9


__use `PHPhotoLibrary`__

```
// need @import Photos;

- (void)saveImageToPhotoAlbum3:(UIImage *)image
{
    __block PHObjectPlaceholder *placeholder = nil;
    
    [[PHPhotoLibrary sharedPhotoLibrary] performChanges:^{
        
        PHAssetChangeRequest *request = [PHAssetChangeRequest creationRequestForAssetFromImage:image];
        placeholder = request.placeholderForCreatedAsset;
        
    } completionHandler:^(BOOL success, NSError * _Nullable error) {
        
        PHFetchResult<PHAsset *> *result = [PHAsset fetchAssetsWithLocalIdentifiers:@[placeholder.localIdentifier] options:nil];
        
        PHAsset *asset = result.firstObject;
        
        // do watver with PHAsset
        
        // note: this completionHandler runs on arbitrary queue
        
    }];
}
```

## 5-23

proper way do UITextField text change call back

```
textField addTarget:self 
             action:@selector(textFieldDidChange:) 
   forControlEvents:UIControlEventEditingChanged];
```

## 5-20

Most reliable way to adjust UITableView cell separator insets

```
// where you can set it in cellForRowAtIndexPath
// or in cell's awakeFromNib
cell.separatorInset = UIEdgeInsetsMake(0, 50, 0, 0);

```

## 5-17

Interesting links

* [This is why most mobile development projects fail](http://clean-swift.com/mobile-development-projects-fail/)
* [NSNumberFormatter](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSNumberFormatter_Class/) use this to show currency base on current locale

```
NSNumber *someNumber = [NSNumber numberWithDouble:total];

NSNumberFormatter *nf = [[NSNumberFormatter alloc] init];
[nf setNumberStyle:NSNumberFormatterCurrencyStyle];
NSString *someString = [nf stringFromNumber:someNumber];
```

## 5-12

Interesting links

* [ELI5: Why do some organs come in pairs, like Kidneys and Lungs, but others are singular, such as the Liver or Heart?](https://www.reddit.com/r/explainlikeimfive/comments/4iu3xq/eli5_why_do_some_organs_come_in_pairs_like/)
* [The easy & reliable way of handling UITableView insets when the keyboard is shown](https://gist.github.com/TimMedcalf/9505416)
* [5:2 diet - 2 days of low calorie(like 600ish for men), 5 days of normal calorie](https://en.wikipedia.org/wiki/5:2_diet)
* [Soylent or soylent alternatives for healthy meal replacement, gaining muscle, and saving money?](https://www.reddit.com/r/Fitness/comments/4haetk/soylent_or_soylent_alternatives_for_healthy_meal/)
* 

## 5-7

Good stuff from surfing

* [Software Engineering Podcasts Review](https://www.reddit.com/r/programming/comments/4hycnz/software_engineering_podcasts_review/)
* [A Guide to Bayesian Statistics](https://news.ycombinator.com/item?id=11613877)

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




