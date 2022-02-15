# EMAIL-DARKMODE
These different techniques for dark mode were initiated by Nicole Merlin, Remi Parmentier, Mark Robbins, Jay Oram and some other email geeks, and here is a summary of all these techniques known and still functional in 2022. I will do my best to keep this page up to date, please feel free to report errors or outdated items over time..

**NO SUPPORT: Gmail app and Windows 10 mail.** 

for other darkmode clients, here are some hacks


## Image Swap (Code from Litmus team)

>This works on 
- :heavy_check_mark: Office 365 Dark (macOS)
- :heavy_check_mark: Android 10 - Gmail Dark  
- :heavy_check_mark: iPhone SE dark - Outlook 
- :heavy_check_mark: Outlook - Chrome (dark)

>Don't works on
- :x: Android 12 - Gmail Dark 
- :x: Office 365 Dark - (win)
- :x: iPhone 12 iOS 14 (force dark) 
- :x: iPhone 12 - Gmail iOS 14 (dark)

In the head
```
<meta name="color-scheme" content="light dark">
<meta name="supported-color-schemes" content="light dark">
```
In the style block

```
@media (prefers-color-scheme: dark ) {
/* Shows Dark Mode-Only Content, Like Images */
.dark-img { display:block !important; width: auto !important; overflow: visible !important; float: none !important; max-height:inherit !important; max-width:inherit !important; line-height: auto !important; margin-top:0px !important; visibility:inherit !important; }
   
/* Hides Light Mode-Only Content, Like Images */
.light-img { display:none; display:none !important; }
}
```

For Outlook App
```
/* Shows Dark Mode-Only Content, Like Images */
[data-ogsc] .dark-img { display:block !important; width: auto !important; overflow: visible !important; float: none !important; max-height:inherit !important; max-width:inherit !important; line-height: auto !important; margin-top:0px !important; visibility:inherit !important; }
 
/* Hides Light Mode-Only Content, Like Images */
[data-ogsc] .light-img { display:none; display:none !important; }
```

Then in the html :

```
<img class="light-img" src="https://campaigns.litmus.com/_email/_global/images/logo_icon-name-black.png" width="163" height="60" alt="Litmus" style="color: #33373E; font-family:'proxima_nova', Helvetica, Arial, sans-serif; text-align:center; font-weight:bold; font-size:36px; line-height:40px; text-decoration: none; margin: 0 auto; padding: 0;" border="0" />
 <!-- The following Dark Mode logo image is hidden with MSO conditional code and inline CSS, but will be revealed once Dark Mode is triggered -->
 
<!--[if !mso]><!----><div class="dark-img" style="display:none; overflow:hidden; float:left; width:0px; max-height:0px; max-width:0px; line-height:0px; visibility:hidden;" align="center">
<img src="https://campaigns.litmus.com/_email/_global/images/logo_icon-name-white.png" width="163" height="60" alt="Litmus" style="color: #ffffff; font-family:'proxima_nova', Helvetica, Arial, sans-serif; text-align:center; font-weight:bold; font-size:36px; line-height:40px; text-decoration: none; margin: 0 auto; padding: 0;" border="0" />
</div><!--<![endif]-->
```
**Note**:

It's working on Mac OS so on Mac OS Monterrey, Big Sur, Mojave you will have the white image. The background won't change on these versions so to avoid white image on light background you'll have to change the background color of the container.
If you choose light mode, there won't be any changes on Mac OS so on Mac OS Monterrey, Big Sur, Mojave (so you'll have the dark image on light background)

```
<meta name="color-scheme" content="light">
<meta name="supported-color-schemes" content="light">
<style>
:root {
	color-scheme: light;
	supported-color-schemes: light;
}
```

For more informations, please check [Litmus :Ultimate Guide to Dark Mode](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers/).
	
## Image swap (hack and code from Mark Robbins)

>This works on 
- :heavy_check_mark: Office 365 Dark (macOS)
- :heavy_check_mark: Android 10 - Gmail Dark  

>Don't works on
- :x: Android 12 - Gmail Dark 
- :x: Office 365 Dark - (win)
- :x: iPhone 12 iOS 14 (force dark) 
- :x: iPhone 12 - Gmail iOS 14 (dark)
- :x: Outlook - Chrome (dark)
- :x: iPhone SE dark - Outlook 

```
<picture>
  <source srcset="dark-img.png" media="(prefers-color-scheme: dark)">
  <img src="light-img.png" alt="Alt Text!" style="">
</picture>
```

**Note**:

It's working on Mac OS so on Mac OS Monterrey, Big Sur, Mojave so you will have the white image. The background won't change so here Remi adds a wrapping div with the "email-dark-background" class to change the background color. 
If you choose light mode (see below), there won't be any changes on Mac OS so on Mac OS Monterrey, Big Sur, Mojave (so you'll have the dark image on light background)

```
<meta name="color-scheme" content="light">
<meta name="supported-color-schemes" content="light">
<style>
:root {
	color-scheme: light;
	supported-color-schemes: light;
}
```
For more information on image swap, please check [Mark Robbins' page](https://www.goodemailcode.com/email-enhancements/picture) and original [webkit page](https://webkit.org/blog/8840/dark-mode-support-in-webkit/)

## Image swap (hack and code from Remi Parmentier)

Exact same result as above 

>This works on 
- :heavy_check_mark: Office 365 Dark (macOS)
- :heavy_check_mark: Android 10 - Gmail Dark  
- :heavy_check_mark: Outlook - Chrome (dark)

>Don't works on
- :x: Android 12 - Gmail Dark 
- :x: Office 365 Dark - (win)
- :x: iPhone 12 iOS 14 (force dark) 
- :x: iPhone 12 - Gmail iOS 14 (dark)  
-  :x: iPhone SE dark - Outlook 

In the html:
```
<!-- wrapping div -->
<div lang="en" style="padding:32px 16px; background-color:#f7f7f7;" class="email-dark-background">
<!-- wrapping div -->

<div style="margin:auto; text-align:center; width:205px; height:165px;" class="email-picture">
<picture>
	<source srcset="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-dark.png" media="(prefers-color-scheme:dark)" />
	<img src="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-light.png" width="205" height="165" alt="DuckDuckGo" style="vertical-align:middle; max-width:100%; height:auto; font:1em sans-serif; color:#000;" />
</picture>
</div>
...
</div>
```
In the style block :
```
@media (prefers-color-scheme:dark) {
	.email-dark-background:not([class^="x_"]) { color:#fff !important; background-color:#1c1c1c !important; }
	.email-picture:not([class^="x_"]) img { color:#fff !important; }
}
</style>
<style id="css-dark-mode-outlook-com">
	[data-ogsb] { color:#fff !important; background-color:#1c1c1c !important; }
	[data-ogsb] .email-picture { background:url('https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-dark.png') no-repeat center; background-size:contain; }
	[data-ogsb] .email-picture img { visibility:hidden; }
</style>
```

**Note**:

It's working on Mac OS so on Mac OS Monterrey, Big Sur, Mojave so you will have the white image. The background won't change so here Remi adds a wrapping div with the "email-dark-background" class to change the background color. 
If you choose light mode (see below), there won't be any changes on Mac OS so on Mac OS Monterrey, Big Sur, Mojave (so you'll have the dark image on light background)

```
<meta name="color-scheme" content="light">
<meta name="supported-color-schemes" content="light">
<style>
:root {
	color-scheme: light;
	supported-color-schemes: light;
}
```
To see the original code, please check [hteumeuleu's codepen](https://codepen.io/hteumeuleu/pen/porJdjR)

## Image swap (from testi@log)

>This works on 
- :heavy_check_mark: iPhone 12 iOS 14 (force dark)

Following Nicole Hickman remark on EmailSlack about iPhone 12 iOS 14 (dark), Hussein Al Hammad spoted testi@ log in which we can read : "iPhone 12 iOS 14 (dark) is since march 2021 (force dark) by adding to <html> class ".apple-mail-implicit-dark-support".
	
So to simply target iPhone 12 iOS 14 (dark) we could do 

In the html:
```
<img class="light-img" alt="" border="0" width="94" height="25" src="ligth-image.png" style="width:94px;height:25px">
<img class="dark-img" alt="" border="0" width="94" height="25" src="dark-image.png" style="width:94px;height:25px;display:none">
```
In the style block:
```
.apple-mail-implicit-dark-support .dark-img{
	display:block !important
	
}
.apple-mail-implicit-dark-support .light-img{
	display:none !important;
} 
```

## Image swap 
	
Including the last hack + the `<picture>` solutions above, we can get a quite good support for darkmode :

>This works on 
- :heavy_check_mark: Office 365 Dark (macOS)
- :heavy_check_mark: Android 10 - Gmail Dark  
- :heavy_check_mark: Outlook - Chrome (dark)
- :heavy_check_mark: iPhone SE dark - Outlook 
- :heavy_check_mark: iPhone 12 iOS 14 (force dark)
	
>Don't works on
- :x: Android 12 - Gmail Dark 
- :x: Office 365 Dark - (win) 
- :x: iPhone 12 - Gmail iOS 14 (dark) 
	
In the style block :
```
<style>
   [data-ogsb] { 
      color:#fff !important; 
      background-color:#1c1c1c !important; 
   }
   [data-ogsb] .swap-image,
    .apple-mail-implicit-dark-support .swap-image{
      background: url('image-for-darkmode.png') no-repeat center;
      background-size: contain;
    }
    [data-ogsb] .swap-image img,
     .apple-mail-implicit-dark-support .swap-image img{
      visibility: hidden;
    }
</style>
```
And inline : 
```
<div class="swap-image">
    <picture>
      <source srcset="image-for-darkmode.png" media="(prefers-color-scheme: dark)">
      <img src="regular-image.png" alt="Alt Text!" width="94" height="25" border="0" style="width:94px;height:24px;color: #ffffff; font-family: Arial, sans-serif; text-align:left; font-size:28px; line-height:36px; text-decoration: none; margin: 0 auto; padding: 0;">
    </picture>
  </div>
```
## Keep text color 
	
>This works on 
- :heavy_check_mark: iPhone 12 iOS 14 (force dark)
	
With the class described above, we can also target iPhone 12 iOs 14 (force dark) and force text color to remain the same on darkmode.
Example with white color : 

```
.apple-mail-implicit-dark-support .mytitle,
.apple-mail-implicit-dark-support .subtitle{
	color:#ffffff !important;
	-webkit-text-fill-color: #ffffff !important; /*without this is doesn't work */
}
```

## Darkmode : Fixing problems in dark mode (hacks and code from Nicole Merlin)

The following techniques were discovered and popularized by Nicoles Merlin through the articles she wrote on Envato (link at the end of each chapter).All the code come directly from the article on the envato website and all credits go to Envato articles. I put the reference link under each part

### MSO Gradient Solution to keep text colors in html

>This works on 
- :heavy_check_mark: Office 365 Dark (Win)

To Preserve the Color of Text in Darkmode, we can add a class to the code we want to fix. 
For example, for a white text, in the code :

`<p class="keep-white" style="color:#ffffff;">This text will remain WHITE</p>`

In the style block:
```
<!--[if gte mso 16]>
    <style>
        .keep-white {
            mso-style-textfill-type:gradient;
            mso-style-textfill-fill-gradientfill-stoplist:"0 \#FFFFFF 0 100000\,100000 \#FFFFFF 0 100000";
            color:#000000 !important;
        }
    </style>
<![endif]-->
```

Or for a black text, in the code:

`<p class="keep-black" style="color:#000000;">This text will remain BLACK</p>`

In the style block:
```
<!--[if gte mso 16]>
    <style>
        .keep-black {
            mso-style-textfill-type:gradient;
	    mso-style-textfill-fill-gradientfill-stoplist:"0 \#000000 1 100000\,99000 \#000000 1 100000";
            color:#ffffff !important;
        }
    </style>
<![endif]-->
```
For more information on this, read Nicole Merlin article : [How To Fix Outlook Dark Mode Problems (Email Design)](https://webdesign.tutsplus.com/tutorials/how-to-fix-outlook-dark-mode-problems--cms-37718)
	
### MSO Gradient Solution to keep background colors in html

>This works on 
- :heavy_check_mark: Office 365 Dark (Win)
	
Following Nicole's tutorial, I noticed that this technique also works for the background color. For example :
For a black button on outlook that becomes white in darkmode
	
```
<!--[if gte mso 16]>
    <style>
        .button {
		mso-style-textfill-type:gradient;
            	mso-style-textfill-fill-gradientfill-stoplist:"0 \#FFFFFF 0 100000\,100000 \#FFFFFF 0 100000";
		background-color:black !important;
        }
    </style>
<![endif]-->
```

### Different Solutions to Keep text colors on VML

>This works on 
- :heavy_check_mark: All Outlook that support VML

**solution 1**

The following style attribute can be tested :
```
mso-style-textfill-fill-color:#ffffff;
```

**solution 2**

- According to Nicole Merlin, we can use CSS positioning and z-index to layer the email content over the top of the VML content. Thus the text content remain separate from the  VML. 
- Alternativly, we can use the `mso-style-textfill-type:gradient` trick describe above
 

**solution 3 : use the mso style attribute: mso-color-alt**

 **In case of a White Text**
 
 Nicole Merlin made some tests and found that :
- The body background must be #555555 or lighter
- VML fill must be `#333333` or darker

Example :

```
<body style="background-color:#555555;">
```

Or in the style block
  
```
  <!--[if gte mso 16]>
    <style>
        body {
            background-color:#555555 !important;
        }
    </style>
<![endif]-->
```

In the vml part, we must ensure that the vml element is dark :
  
`<v:rect fillcolor="#333333">` or `<v:fill type="frame" src="image.jpg" color="#333333" />`

Then in the code `<p style="margin:0;color:#ffffff;mso-color-alt:auto;">White text</p>` 

Or we can instead use a class `<p class="vml-white" style="margin:0;color:#ffffff;">White text</p>`

And in the style block
```
  <!--[if gte mso 16]>
    <style>
        .vml-white {
            mso-color-alt: auto;
        }
    </style>
<![endif]-->
```
  
**In case of a Black Text**

Same thing, here :
- the body background must be #444444 or darker
- the VML fill must be #555555 or lighter

Example : We can put the background-color direclty on a container tag
`<body style="background-color:#444444;">`

Or in the style block
```
  <!--[if gte mso 16]>
    <style>
        body {
            background-color:#444444 !important;
        }
    </style>
<![endif]-->
```
And in the vml shape add a dark fillcolor `<v:rect fillcolor="#555555">`

or in case of a v:fill element, add a dark color :

`<v:fill type="frame" src="image.jpg" color="#555555" />`  

And in the html element,

`<p style="margin:0;color:#000000;mso-color-alt:auto;">Black text</p>`
  
Or if we prefer, with a class on the tag:
  
`<p class="vml-black" style="margin:0;color:#000000;">Black text</p>`
  
And in the style block : 

```
<!--[if gte mso 16]>
    <style>
        .vml-black {
            mso-color-alt: auto;
        }
    </style>
<![endif]-->
```

On top of that, Nicole Merlin reported to me Alex Robinson's discovery which he shared on twitter:(quote) "It turns out you can keep the vml fill transparent while satisfying the light/dark fill requirement. eg <v:rect fillcolor="#555555" opacity="0%">" .[See the message](https://twitter.com/AlexRob22358708/status/1490879213679050752)

For more information on this read Nicole Merlin article : [Fixing Text Color Changes Inside VML](https://webdesign.tutsplus.com/tutorials/how-to-fix-outlook-dark-mode-problems--cms-37718)

### Buttons
  
#### Fix Buttons With a Different Colour Behind the Text in Dark Mode 

#### Transparent borders

>This work on:
- :heavy_check_mark: Outlook.com Webmail, 
- :heavy_check_mark: Outlook for iOS, 
- :heavy_check_mark: Outlook for Android

Another technique from Nicole Merlin : we can make the border transparent, e.g. `border: 8px solid transparent` so that only the background colour of the link element shows through

#### Transparent background
>This work on
- :heavy_check_mark: Office 365 Dark (Win)

According to Nicole, we can make the <a> tag’s background transparent for Outlook only. We can do it by adding the conditional CSS to the head of the template.

For example, if the link has a class of `mylink`, we can include the following in the style block:
  
```
<!--[if mso]>
    <style>
        .mylink {background: transparent !important;}
    </style>
<![endif]-->
```
For more information on this read Nicole Merlin article on [How to Fix Common Problems With Buttons in Dark Mode](https://webdesign.tutsplus.com/articles/fixing-problems-with-buttons-in-dark-mode-email-design--cms-39411)

	
### Borders

#### Fix Buttons Disappearing Into the Background in Dark Mode

>This works on 
- :heavy_check_mark: Gmail App for iOS/Android
- :heavy_check_mark: Outlook App for iOS/Android  
- :heavy_check_mark: Outlook for Mac
- :heavy_check_mark: Outlook.com
  
These email clients will keep the button dark but they will also flip the body background. This might cause issues as the button’s edges become invisible.
 Here are some advices taken from Nicole's Envato article :
	
  >- "Try adding a border to the outside of your button in the same colour as the background in light mode. Many email clients don’t alter CSS border colours when they process colours for Dark Mode."
>  - "Try using the CSS outline property instead of the border property if you have a square button, and you can also fake a border by nesting a button inside a slightly padded element and applying a background to that". 
>  - "By using a background image or a linear-gradient, you can actually ensure that the colour of the fake border doesn’t change."
  
  
More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

#### Using Media Queries to Control Borders in Dark Mode
	
>This work on
- :heavy_check_mark: Apple Mail (iOS and macOS)
	
For borders, one simple Nicole advice is to force color through darkmode media queries 

```
  <style>
    @media (prefers-color-scheme: dark) {
        .borders {border-color: #fafafa !important;}
    }
</style>
```

#### Using Data Attributes to Fix Borders in Dark Mode
	
>This work on
- :heavy_check_mark: outlook.com
- :heavy_check_mark: Outlook Apps for iOS
- :heavy_check_mark: Outlook Apps for Android

In the code
	
```
<td class="my-border" style="border:2px solid #000000;padding:30px 40px;">
```
  In the style block :
		
 ```
  <style>
    [data-ogsc] .my-border, 
    [data-ogsc] .my-border .btnlink {
        border: 2px solid white !important;
    }
</style>
```

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)
	
### Fix Border Problems in Outlook for Mac

>This work on
- :heavy_check_mark: Outlook for Mac

> "Outlook for Mac does tend to invert border colors but it keeps dark backgrounds dark on tables and cells, but not on divs, paragraphs or link tags. So where possible, add borders to div".

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

### Fix Border Problems in Outlook for Windows

>This work on
- :heavy_check_mark: Outlook for Windows

Here we can try Outlook specific code for borders, like `mso-border-alt`:
	
```border:2px solid #000000;mso-border-alt:2px solid #ffffff;```

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)
	
#### Different Elements to Fix Border Problems 
 Here are some other advices from Nicole, direclty taken from her darkmode article
	
- Adjust the colors slightly eg `#ffffff` to `#fafafa` or `#000000` to `#111111`.
	
- Try Outline if You Are Working With Square Edges

>This work on
- :heavy_check_mark: Windows Live Mail
- :heavy_check_mark: Gmail app (iOS)
- :heavy_check_mark: Microsoft365 Outlook for Windows
		
```
<td style="outline:2px solid #ffffff;border:2px solid #000000;">
```

- Try a Box-Shadow

>This work on
- :heavy_check_mark: Apple Mail (iOS)
- :heavy_check_mark: Apple Mail (macOS)
- :heavy_check_mark: Outlook for Mac
		
 ```
box-shadow: 0px 0px 0px 2px #ffffff;` or `box-shadow: inset 0px 0px 0px 2px #ffffff;
```

- Try Using CSS Blend Modes

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

## Gmail’s dark mode in iOS (Hack and Code from Remi Parmentier)

```	
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fixing Gmail’s dark mode issues with CSS Blend Modes</title>
    <style>
        u + .body .gmail-blend-screen { background:#000; mix-blend-mode:screen; }
        u + .body .gmail-blend-difference { background:#000; mix-blend-mode:difference; }
    </style>
</head>
<body class="body">
    <div style="background:#639; background-image:linear-gradient(#639,#639); color:#fff;">
        <div class="gmail-blend-screen">
            <div class="gmail-blend-difference">
                <!-- Your content starts here -->
                Lorem ipsum dolor, sit amet, consectetur adipisicing elit.
                <!-- Your content ends here -->
            </div>
        </div>
    </div>
</body>
</html>
```
For more information on blend mode please check [Remi Parmentier' page](https://www.hteumeuleu.com/2021/fixing-gmail-dark-mode-css-blend-modes/)
	

## Image color inersion (hack and code from Jay Oram)
	
>This works on 
- :heavy_check_mark:Office 365 Dark (macOS)
- :heavy_check_mark:Apple mail / iOS 
	
```
@media (prefers-color-scheme: dark) {
.foo {filter: brightness(0) invert(1);} 
}
```
For more information, please check [Jay Oram](https://www.emailtalk.fm/episodes/08-dark-mode-w-jay-oram).

## Add a drop shadow

A common hack to add a white shadow around an image in dark mode

>This only works on 
- :heavy_check_mark: Office 365 Dark (macOS)

```	
@media (prefers-color-scheme: dark) {
.foo {filter: drop-shadow(0px 0px 10px rgba(255,255,255,0.6)) 
  drop-shadow(0px 0px 10px rgba(255,255,255,0.6))
  drop-shadow(0px 0px 10px rgba(255,255,255,0.6));} 
} 
```
	
## override macOS/iOS dark mode colors
>This works on 
- :heavy_check_mark: macOS/iOS
- :heavy_check_mark: Outlook on Mac 

This code and text comes directly from Brian Thies on [Litmus](https://litmus.com/community/discussions/8160-ios13-dark-mode-inverting-all-colors-in-e-mail-how-to-disable#comment-16241)

For background colors, use a one color gradient:
```
background-image: linear-gradient(#ffffff,#ffffff)
```

For text, use this along with your standard color style:

```
-webkit-text-fill-color: #000000 !important;
```

For borders, include original border style plus...

```
-webkit-border-before: 2px solid #000000 !important; (use for top border)
-webkit-border-after: 2px solid #000000 !important; (use for bottom border)
-webkit-border-start: 2px solid #000000 !important; (use for left border)
-webkit-border-end: 2px solid #000000 !important; (use for right border)
```
