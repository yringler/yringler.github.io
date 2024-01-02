[Flutter web](https://flutter.dev/web) is coming. It promises excellent run time performance, smooth animations, elegant interface design -but at what cost? Flutter web is not production ready yet, so we have to cut it some slack, but looking at some [basic demos](https://minikin.me/flutter-web-demo/#/) show the main JS file weighing in at around 1MB, or 300KB gzipped. This isn’t totally unworkable, and we can expect some improvement by the time it hits production (for example, %40 of the JS file isn’t run and should be optimized out), but this still puts flutter at to upper end of web frameworks in terms of file size. And this is just a relatively small demo.

That does not mean that flutter web should be avoided.

People are very smart, and can do very cool things. One cool thing that people do is build sand castles. Very [big sand castles](https://m.escapehere.com/inspiration/the-10-coolest-sandcastle-competitions-in-the-world/). Now, sand is a wonderful substance. You can write letters in it pretty easily. A simple painting isn’t out of the question. But what these people do with the stuff simply defies the imaginative abilities of regular mortals.

HTML is a very capable system. You create content, divide it into parts, add headings and lists, pictures and menus. Even audio and video is right at home. _It is not built for more than that._ It stands for Hyper Text Markup Language, which is a fancy way of saying “good looking text which can link to other text.” When HTML was created, in the early dawn of the internet, it was strictly a text medium.

HTML is very good at text.

Fast forward a few decades, the internet became very successful (as you may have heard), and HTML is still with us. People are building fantastic things with it, such as [Google Docs](https://www.google.com/docs/about/), even really full featured [super powered text editors](https://code.visualstudio.com/). They even are maintainable, and are reasonable to read and write, with [many](https://angular.io/) [excellent](https://vuejs.org/) [frameworks](https://reactjs.org/) ([et](https://svelte.dev/). [al.](https://mithril.js.org/index.html)).

You can make a castle out of sand. You can make anything you imagine out of HTML. And just like there are tools to make sand craftsmanship easier, there are also tools which make HTML easier. That doesn’t mean that it’s a good idea. Actually, it’s a really bad idea. We as web developers are taking a technology way out of the purpose it’s designed for, and it’s time to look to newer technologies that were created and battle tested with the challenges of modern UI in mind.

That newer technology is flutter. Flutter on the web isn’t for traditional web uses. The flutter project itself is very open about this.

> Not every HTML scenario is ideally suited for Flutter at this time. For example, text-rich flow-based content such as blog articles benefit from the document-centric model that the web is built around, rather than the app-centric services that a UI framework like Flutter can deliver.
> 
> [flutter.dev/web](https://flutter.dev/web)

Ultimately, flutter, like any denizen of the web, has to render to HTML, but with a key difference. In other frameworks, ultimately the developer is consciously dealing with HTML/CSS. In flutter it’s completely abstracted away into flutter’s [widget](https://flutter.dev/docs/resources/architectural-overview#widgets) system, empowering developers to fully break loose from the their text-centric chains.

Flutter, and the [dart language](https://dart.dev/guides/language/language-tour) powering it, is built to create crazy awesome UI experiences. Like [Rive](https://rive.app/). Rive is a fully featured animation studio and more, which was rewritten in flutter. Could such a thing be done in HTML? Absolutely. But why? Why do we insist on pumping up old tech stacks when there are new, powerful, purpose built tools now available? We could toughen up a blade of grass and slay any problem with it. It’s time to wield a sword.

(Well, now quite yet, because flutter web is still in beta, but you know what I mean.)