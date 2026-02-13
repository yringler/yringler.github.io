---
date: 2020-08-19T00:00:00-05:00
slug: "flutter-navigation-material"
title: "Flutter Navigation Material"
tags: [coding]
---

To my great consternation, route transition animations broke after upgrading the app â€“ when going from one section to another, the old one was visible behind the new one until the transition was finished, and it looked terrible. I could not think what could be the problem.

Then, out of the blue (well, after [breaking my head on it](https://quoteinvestigator.com/2012/07/21/luck-hard-work/) for a while), it hit me â€“ I didnâ€™t have any [material](https://material.io/design/environment/surfaces.html#material-environment)!

_(A bit of background â€“ in the material design system, everything is based on material, which is inspired by how things work in the real world._

1.  _Imagine a sheet of paper._
2.  _Now, cut a button from another piece of paper._
3.  _Put the button on the first sheet._

_Now you have a button, which is made from material, on top of the rest of your design, which is also a piece of material.)_

The routing had been [based](https://github.com/yringler/inside-app/blob/763b1e81ee4a421a4a1cea6b66cea1b783b4ca3f/lib/main.dart#L63) on [MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html). With the update, it used [Navigator](https://api.flutter.dev/flutter/widgets/Navigator-class.html) instead. _MaterialApp_ gives you some material to fall back on â€“ it is, after all, a [material](https://material.io/design/environment/surfaces.html#material-environment) app. _Navigator_ â€“ not so much. In upgrading, I had dropped the material that the whole app was built on!

Lesson learned: when youâ€™re growing, donâ€™t lose your roots.

> Between one level and the next, before he can reach the higher one, he is in a state of decline from his previous levelâ€¦  
> This is considered a decline only relative to his former state, and not (Gâ€‘d forbid) relative to all other men; for he still surpasses them in his divine serviceâ€¦  
> For the mainstay of his service while he is in this fallen state is the love of Gâ€‘d in which he had been educated and trained from his youth
> 
> [Rabbi Shneur Zalman of Liadi](https://www.chabad.org/library/article_cdo/aid/110437/jewish/The-Alter-Rebbe.htm), â€œThe Alter Rebbeâ€, [Tanya, _Chinuch Katan_](https://www.chabad.org/library/tanya/tanya_cdo/aid/45259/jewish/Introduction.htm)