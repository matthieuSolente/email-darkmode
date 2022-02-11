# EMAIL-DARKMODE
These different techniques for dark mode were initiated by Nicole Merlin, Remi Parmentier, Mark Robbins and some other email geeks, and here is a summary of all these techniques known and still functional in 2022. I will do my best to keep this page up to date, please not to point out errors or deprecated elements over time.

**NO SUPPORT: Gmail app and Windows 10 mail. ** 

for other darkmode clients, here are some hacks


## Image Swap (Code from Litmus team)
This works on 
- Andoird 10 Gmail Dark 
- Iphone SE Dark Outlook 
- Office 365 Dark Mac OS

Don't work on
- Android 12 gmail dark
- Outlook chrome dark webmail
- Iphone 12 ios 14 force Darkmode
- Office 365 Dark Windows
- Mac OS Monterrey, Big Sur, Mojave no changes.

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

For more informations, please check [Litmus :Ultimate Guide to Dark Mode](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers/).

## Image swap (hack from Mark Robbins)
This technique will work on Apple Mail, Outlook for Mac	
```
<picture>
  <source srcset="dark-img.png" media="(prefers-color-scheme: dark)">
  <img src="light-img.png" alt="Alt Text!" style="">
</picture>
```
For more information on image swap, please check [Mark Robbins](https://www.goodemailcode.com/email-enhancements/picture)

## Image swap (hack from Remi Parmentier)

In the html:
```
<div style="margin:auto; text-align:center; width:205px; height:165px;" class="email-picture">
<picture>
	<source srcset="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-dark.png" media="(prefers-color-scheme:dark)" />
	<img src="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-light.png" width="205" height="165" alt="DuckDuckGo" style="vertical-align:middle; max-width:100%; height:auto; font:1em sans-serif; color:#000;" />
</picture>
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

## Darkmode : Outlook 365 dark mode (All code from Nicole Merlin)

### MSO Gradient Solution

Add a class to the code you want to fix. 
In the code :
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

### Darkmode : Keeps colors unchanged on VML

**solution 1**

```
mso-style-textfill-fill-color:#ffffff;
```

**solution 2**

- use CSS positioning and z-index to layer your email content over the top of your VML content, keeping your text content separate from your VML. 
- use the `mso-style-textfill-type:gradient` trick
 
**solution 3**

 **If You Need White Text**
- Body background must be #555555 or lighter
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
  
  Then ensure your vml element is dark
  
```
<v:rect fillcolor="#333333">` or `<v:fill type="frame" src="image.jpg" color="#333333" />
```
Then in the code
 
 ```
 <p style="margin:0;color:#ffffff;mso-color-alt:auto;">White text</p>
 ```

Or with a class
```
<p class="vml-white" style="margin:0;color:#ffffff;">White text</p>
```
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
  
**If You Need Black Text**

Body background must be #444444 or darker
VML fill must be #555555 or lighter

example : direclty on a container tag
```
<body style="background-color:#444444;">
```
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
  And in the vml shape
  
```
<v:rect fillcolor="#555555">
```
or 
```
<v:fill type="frame" src="image.jpg" color="#555555" />
```  

And in the html

```
<p style="margin:0;color:#000000;mso-color-alt:auto;">Black text</p>
```
  
Or with a class :
  
```
<p class="vml-black" style="margin:0;color:#000000;">Black text</p>
```
  
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

### Buttons
  
#### Fix Buttons With a Different Colour Behind the Text in Dark Mode in Outlook.com Webmail, Outlook for iOS, or Outlook for Android
Make the border transparent, e.g. border: 8px solid transparent so that only the background colour of the link element shows through
  
In the case of a vml button, if the borders of the html link stand out or if the background of the link is different, simply add the following rule:

<!--[if mso]> <style type="text/css">
.btn{background:transparent !important;border:none !important} </style> <![endif]-->
For borders, include original border style plus...

### In Outlook for Windows in Dark Mode
Make the <a> tag’s background transparent for Outlook only. You can do this by adding conditional CSS to the head of your email.

For example, if you have a link like this with a class of buttonlink: '<a class="buttonlink">' you would include the following in the head of your email:
  
```
<!--[if mso]>
    <style>
        .buttonlink {background: transparent !important;}
    </style>
<![endif]-->
```

### Fix Buttons Disappearing Into the Background in Dark Mode : Gmail App for iOS/Android / Outlook App for iOS/Android / Outlook for Mac / at Outlook.com
  
These email clients will keep your button dark but flip the body background to be dark as well. Suddenly, your dark button’s edges are invisible.
  
  - Try adding a border to the outside of your button in the same colour as the background in light mode. Many email clients don’t alter CSS border colours when they process colours for Dark Mo
  - Try using the CSS outline property instead of the border property if you have a square button, and you can also fake a border by nesting a button inside a slightly padded element and applying a background to that. 
  - By using a background image or a linear-gradient, you can actually ensure that the colour of the fake border doesn’t change.
  
  
### Borders

#### Using Media Queries to Control Borders in Dark Mode in Apple Mail (iOS and macOS)
	
Example in the style block 
```
  <style>
    @media (prefers-color-scheme: dark) {
        .borders {border-color: #fafafa !important;}
    }
</style>
```

#### Using Data Attributes to Fix Borders in Dark Mode in outlook.com and the Outlook Apps for iOS/Android

In the code
	
```
<td class="oldotcom-border" style="border:2px solid #000000;padding:30px 40px;">
```
  In the style block :
		
 ```
  <style>
    [data-ogsc] .oldotcom-border, 
    [data-ogsc] .oldotcom-border .btnlink {
        border: 2px solid white !important;
    }
</style>
```
#### Using Different Elements to Fix Border Problems in Outlook for Mac
  Outlook for Mac does tend to invert border colors but it keeps dark backgrounds dark
  
- Try Outline if You Are Working With Square Edges
		
```
<td style="outline:2px solid #ffffff;border:2px solid #000000;">
```
- Try a Box-Shadow
		
 ```
box-shadow: 0px 0px 0px 2px #ffffff;` or `box-shadow: inset 0px 0px 0px 2px #ffffff;
```
- Try Using CSS Blend Modes
	
For more informations on all theses techniques, please check : [Darkmode Problems](https://webdesign.tutsplus.com/tutorials/how-to-fix-outlook-dark-mode-problems--cms-37718)
	[Buttons in darkmode](https://webdesign.tutsplus.com/articles/fixing-problems-with-buttons-in-dark-mode-email-design--cms-39411)
	[Borders in darkmode](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)
	

## Gmail’s dark mode in iOS (Code from Remi Parmentier)

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
For more information on blend mode please check [Remi Parmentier](https://www.hteumeuleu.com/2021/fixing-gmail-dark-mode-css-blend-modes/)
	

## Image color inersion (hack from Jay Oram)
	
```
@media (prefers-color-scheme: dark) {
.foo {filter: brightness(0) invert(1);} 
}
```


## Others techniques

A common hack to add a white shadow around an image in dark mode Office 365 Dark Mac OS

```	
@media (prefers-color-scheme: dark) {
.foo {filter: drop-shadow(0px 0px 10px rgba(255,255,255,0.6)) 
  drop-shadow(0px 0px 10px rgba(255,255,255,0.6))
  drop-shadow(0px 0px 10px rgba(255,255,255,0.6));} 
} 
```
	
For background colors, use a one color gradient:

```
background-image: linear-gradient(#ffffff,#ffffff)
```

For text, use this along with your standard color style:

```
-webkit-text-fill-color: #ffffff !important;
```
	
For borders, include original border style plus...

```
-webkit-border-before: 2px solid #000000 !important; (use for top border) 
-webkit-border-after: 2px solid #000000 !important; (use for bottom border) 
-webkit-border-start: 2px solid #000000 !important; (use for left border) 
-webkit-border-end: 2px solid #000000 !important; (use for right border)
```
