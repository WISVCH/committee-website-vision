This document describes a proposal vision for committee websites developed by Christiaan Huygens.
Please leave any feedback in GitHub issues for thorough discussion.

# Current situation

At the moment committees develop custom websites for their respective committee(-year).
There are a total of 37 committees of which 22 committees have a website at https://commissies.ch.tudelft.nl/ deployed.
The total of websites available is higher than the number of committees, as some committees build a website each year.
An estimation of the total number of websites currently deployed is ~40.

## Technology choice

Common practice is that a committee appoints one committee member responsible for the website.
This committee member is tasked to build a full-fledged website with commonly the following characteristics:

1. Logo of the event/committee
2. General information about the event/committee
3. Company logos that sponsor the event/committee
4. Detailed overview of activities for the event
5. Location in the form of an embedded Google Maps
6. List of committee members
7. Judicial information of the study association
8. Sometimes there is also a ticket sale for the event

Usually the designated committee member has limited time available to build the whole website, as he/she has a different role in the committee itself.
Therefore, the committee member chooses a technology that he/she is familiar with to build the website.

As a result of this personal choice, there are currently numerous technologies used in all websites deployed.
Examples of technologies include:

1. Express (https://github.com/WISVCH/HackDelft-website)
2. Polymer (https://github.com/WISVCH/symposium)
3. PHP + Bootstrap (https://github.com/WISVCH/lucie-website)
4. MathJax (https://commissies.ch.tudelft.nl/annucie/)
5. PHP + jQuery (https://commissies.ch.tudelft.nl/dies/)
6. WordPress + jQuery
  * https://commissies.ch.tudelft.nl/gala/
  * https://commissies.ch.tudelft.nl/wiewie/
7. Angular + jQuery (https://commissies.ch.tudelft.nl/verdiepcie/)
8. Bootstrap + jQuery (https://commissies.ch.tudelft.nl/wifi/)
9. jQuery
  * https://businesstour.ch.tudelft.nl/
  * https://commissies.ch.tudelft.nl/chipcie/
  * https://commissies.ch.tudelft.nl/dvhj/)
10. WordPress (https://commissies.ch.tudelft.nl/constantijnhuygens)
11. Broken PHP
  * https://commissies.ch.tudelft.nl/graficie/
  * https://commissies.ch.tudelft.nl/pi/
12. No dependencies (https://commissies.ch.tudelft.nl/sjaarcie/)

Other committee websites are not maintained or only serve a "Hello World"-like response.

The above list shows that jQuery is commonly used in conjunction with various technologies.
PHP is used in plain PHP or WordPress.
Other Javascript solutions are employed such as Express, Polymer, Angular and Bootstrap.

## Identified problems

An investigation in the current situation shows that the responsibility of building a committee website is usually a one-man-job.
As a result of time pressure, technologies are employed that this member is familiar with.
While each technology on its own works, the usecase for each committee website is very similar: there are several sections that show up in every website.
Also jQuery is commonly used, assuming that it is easy to use and it is a small dependency.

# Vision proposal

To solve the problems identified in the current situation, the following vision is proposed:

To reduce the workload for the designated committee members, ready-built solutions must be provided.
These solutions must be generic enough for each website, but should be configurable for each committee.
To streamline this process, a single technology must be chosen to take advantage of the reusability between websites.

## Technology options

There are several options to obtain reusability between websites.

### Server-side rendering framework

At first we could choose to make use a server-side rendering framework or language.
Examples of these frameworks/languages is WordPress or plain PHP as well as Express.
While PHP was popular a couple of years ago, the language itself has severe disadvantages and is not actively taught anymore in the Bachelor Computer Science.
Moreover, server-side rendering is usually not required, as the website is fairly static.

Therefore, opting for a server-side rendering framework is for little benefit while it introduces extra learning costs for new study assocation members.

### Client-side rendering framework

Secondly we could opt for a client-side rendering framework.
Examples include Angular, React, Vue, Polymer.
Some of these frameworks also include server-side rendering.

For the same reasons given in the previous section, client-side rendering has little benefit with again an increased learning curve for new members.

### jQuery

The technology list already includes several websites which are using jQuery, so this is an option too.
However, a lot of the functionality that jQuery offers is also available natively in the browser.
Therefore including an extra dependency for a website while the same functionality is also available in the browser does not make a lot of sense.

Moreover, reusability with jQuery is hard to achieve since event handling and modifications can not easily be transferred to a different website.

### Pure Javascript

Since the websites are mostly static, we can also use pure javascript.
While this would certainly work, pure javascript has again a problem of lack of reusability.
Since JS modules have not shipped yet in browsers, there is no option to modularize the code for a website.
It is possible with modern tools such as WebPack, but research has shown that shipping a large amount of javascript to users has a detrimental effect on it the usability of the website.

### Custom elements

All solutions above have disadvantages for the particular usecase of building reusable committee websites.
Frameworks are tailored for large, dynamic websites, while libraries like jQuery do not offer significant development benefits.

In the recent past, custom elements have been introduced and are being natively implemented by browsers.
Custom elements are very similar to jQuery, but the difference is that custom elements can take advantage of declarative reusable HTML templates.
This means that it is not required to ship complete javascript scripts before content can be shown on the screen.

Custom elements can also take advantage of progressive enhancement by providing an initial HTML definition until an element is upgraded.
The user can therefore already see content while the application is loading, resulting in a nicer user experience

**Note that custom elements do not include Polymer.
While Polymer is a library to take advantage of custom elements, it is not required to build a website with custom elements.
It is therefore possible to build a website with pure custom elements, without any dependency**

## Conclusion

Concluding, the proposal is to employ custom elements to build reusable components that can be used in a committee website.
Reusing these components significantly speeds up the development process of committees, such that they can focus on the content or custom components if they require so.
