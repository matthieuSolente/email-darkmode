# Email-Darkmode Rules

These different techniques for dark mode were initiated by Nicole Merlin, Remi Parmentier, Mark Robbins, Jay Oram and some other email geeks, and here is a summary of all these techniques known and still functional in 2023. I will do my best to keep this page up to date, please feel free to report errors or outdated items over time..

# Image Swap

## Image Swap (Code from Litmus team)

This code was tested on testi@ with inline background-color on body (#fefefe).

<details><summary>Check the support on Testi@</summary>
<p>

>This works on (testi@)

- ✔️ MacOS Ventura Mail (dark)
- ✔️ Mac OS Monterey
- ✔️ MacOS Big Sur (dark)
- ✔️ MacOS Mojave(Dark Mode)
- ✔️ Office 365 Dark(macOS)
- ✔️ Outlook - Chrome (dark)
- ✔️ Iphone SE Dark - Outlook
- ✔️ Android 10 - Gmail Dark
- ✔️ Android 11 - Outlook Dark

>Don't works on (testi@)

- ❌ Outlook 2021 (dark)
- ❌ Windows 11 Mail (dark)
- ❌ Office 365 Dark (Win) (2104)
- ❌ IPhone 12 - Gmail iOS14
- ❌ IPhone 14 - iOS16 (dark)
- ❌ IPhone 12 - iOS 14 (force dark)
- ❌ Android 13 -Gmail Dark
- ❌ Android 12 Gmail Dark
</p>
</details>

	
Add the following meta tags in order to Enable Dark Mode in email client user agents

```html
<meta name="color-scheme" content="light dark">
<meta name="supported-color-schemes" content="light dark">
```

Then add Dark Mode styles for @media (prefers-color-scheme: dark)

```css
@media (prefers-color-scheme: dark ) {
/* Shows Dark Mode-Only Content, Like Images */
.dark-img { display:block !important; width: auto !important; overflow: visible !important; float: none !important; max-height:inherit !important; max-width:inherit !important; line-height: auto !important; margin-top:0px !important; visibility:inherit !important; }
   
/* Hides Light Mode-Only Content, Like Images */
.light-img { display:none; display:none !important; }
}
```

Then to add support to Outlook App (Android), duplicate Dark Mode styles with `[data-ogsc]` prefix

```css
/* Shows Dark Mode-Only Content, Like Images */
[data-ogsc] .dark-img { display:block !important; width: auto !important; overflow: visible !important; float: none !important; max-height:inherit !important; max-width:inherit !important; line-height: auto !important; margin-top:0px !important; visibility:inherit !important; } 

/* Hides Light Mode-Only Content, Like Images */
[data-ogsc] .light-img { display:none; display:none !important; }
```

Then in the html place your two images :

```html
<img class="light-img" src="https://campaigns.litmus.com/_email/_global/images/logo_icon-name-black.png" width="163" height="60" alt="Litmus" style="color: #33373E; font-family:'proxima_nova', Helvetica, Arial, sans-serif; text-align:center; font-weight:bold; font-size:36px; line-height:40px; text-decoration: none; margin: 0 auto; padding: 0;" border="0" />

<!-- The following Dark Mode logo image is hidden with MSO conditional code and inline CSS, but will be revealed once Dark Mode is triggered -->
 
<!--[if !mso]><!----><div class="dark-img" style="display:none; overflow:hidden; float:left; width:0px; max-height:0px; max-width:0px; line-height:0px; visibility:hidden;" align="center">
<img src="https://campaigns.litmus.com/_email/_global/images/logo_icon-name-white.png" width="163" height="60" alt="Litmus" style="color: #ffffff; font-family:'proxima_nova', Helvetica, Arial, sans-serif; text-align:center; font-weight:bold; font-size:36px; line-height:40px; text-decoration: none; margin: 0 auto; padding: 0;" border="0" />
</div><!--<![endif]-->
```

For more informations, please check [Litmus :Ultimate Guide to Dark Mode](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers/).
	
## Image swap (hack and code from Mark Robbins)

This code was tested on Testi@ with inline background-color on body (#fefefe).

<details><summary>Check the support on Testi@</summary>
<p>

>This works on

- ✔️ MacOS Ventura Mail (dark)
- ✔️ Mac OS Monterey
- ✔️ MacOS Big Sur (dark)
- ✔️ MacOS Mojave(Dark Mode)
- ✔️ Office 365 Dark(macOS)

>Don't works on

- ❌ Outlook 2021 (dark)
- ❌ Windows 11 Mail (dark)
- ❌ Office 365 Dark (Win) (2104)
- ❌ IPhone 12 - Gmail iOS14
- ❌ Iphone SE Dark - Outlook
- ❌ IPhone 14 - iOS16 (dark)
- ❌ IPhone 12 - iOS 14 (force dark)
- ❌ Android 11 - Outlook (dark)
- ❌ Android 13 -Gmail Dark
- ❌ Android 12 Gmail Dark
- ❌ Android 10 - Gmail Dark
- ❌ Outlook - Chrome (dark)
</p>
</details>

```html
<picture>
  <source srcset="dark-img.png" media="(prefers-color-scheme: dark)">
  <img src="light-img.png" alt="Alt Text!" style="">
</picture>
```

For more information on image swap, please check [Mark Robbins' page](https://www.goodemailcode.com/email-enhancements/picture) and original [webkit page](https://webkit.org/blog/8840/dark-mode-support-in-webkit/)

## Image swap (hack and code from Remi Parmentier)

This code was tested on Litmus with or without inline background-color on body (#fefefe). 

<details><summary>Check the support on Testi@</summary>
<p>

>This works on 
- ✔️ MacOs Ventura Mail (dark)
- ✔️ MacOs Big Sur (dark)
- ✔️ MacOs Monterey (dark)
- ✔️ MacOs Mojave(Dark Mode)
- ✔️ Iphone SE Dark
- ✔️ Android 11 - Outlook (dark)
- ✔️ Outlook - Chrome (dark)

>Don't works on

- ❌ Android 12 - Outlook 2021 (dark)
- ❌ Windows 11 Mail (dark)
- ❌ Office 365 Dark (Windows)
- ❌ IPhone 12 - Gmail iOS14
- ❌ IPhone 14 - IOS16 (dark)
- ❌ IPhone 12 - iOS 14 (force dark)
- ❌ Android 13 -Gmail Dark
- ❌ Android 12 Gmail Dark
- ❌ Android 10 - Gmail Dark  

</p>
</details>

In the html:

```html
<!-- wrapping div -->
<div lang="en" style="padding:32px 16px; background-color:#f7f7f7;" class="email-dark-background">
    <div style="margin:auto; text-align:center; width:205px; height:165px;" class="email-picture">
        <picture>
            <source srcset="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-dark.png" media="(prefers-color-scheme:dark)" />
            <img src="https://www.hteumeuleu.fr/wp-content/uploads/2021/10/ddg-logo-light.png" width="205" height="165" alt="DuckDuckGo" style="vertical-align:middle; max-width:100%; height:auto; font:1em sans-serif; color:#000;" />
        </picture>
    </div>    
</div>
```
In the style block :

```html
<style>
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

To see the original code, please check [hteumeuleu's codepen](https://codepen.io/hteumeuleu/pen/porJdjR)

## Specific Image swap for iPhone 12 iOS 14 (force dark)

>This works on 
- ✔️ iPhone 12 iOS 14 (force dark)

Following Nicole Hickman remark on EmailSlack about iPhone 12 iOS 14 (dark), Hussein Al Hammad spotted testi@ log in which we can read: "iPhone 12 iOS 14 (dark) is since March 2021 (force dark) by adding the `apple-mail-implicit-dark-support` to the `<html>`", eg. `<html class="apple-mail-implicit-dark-support">`.
	
So to simply target iPhone 12 iOS 14 (dark) we could do something like:

In the HTML:

```html
<img class="light-img" alt="" border="0" width="94" height="25" src="light-image.png" style="width:94px;height:25px">
<img class="dark-img" alt="" border="0" width="94" height="25" src="dark-image.png" style="width:94px;height:25px;display:none">
```

In the style block:

```css
.apple-mail-implicit-dark-support .dark-img {
    display:block !important;
}
.apple-mail-implicit-dark-support .light-img {
    display:none !important;
} 
```

## Specific Image swap for iPhone 12 iOS 14 (force dark) with picture tag
	
Including the last hack + the `<picture>` solutions above, we can get a quite good support for darkmode:

<details><summary>Check the support on Testi@</summary>
<p>

>This works on 
- ✔️ Office 365 Dark(macOS)
- ✔️ MacOS Ventura Mail (dark)
- ✔️ Mac OS Monterey
- ✔️ MacOS Big Sur (dark)
- ✔️ MacOS Mojave(Dark Mode)
- ✔️ Iphone SE Dark - Outlook
- ✔️ IPhone 14 - iOS16 (dark)
- ✔️ IPhone 12 - iOS 14 (force dark)
- ✔️ Android 11 - Outlook (dark)
- ✔️ Outlook - Chrome (dark)
- 
>Don't works on
- ❌ Android 12 - Outlook 2021 (dark)
- ❌ Android 12 - Windows 11 Mail (dark)
- ❌ Android 12 - Office 365 Dark (Win) (2104)
- ❌ Android 12 - IPhone 12 - Gmail iOS14
- ❌ Android 12 - Android 13 -Gmail Dark
- ❌ Android 12 - Android 12 Gmail Dark
- ❌ Android 12 - Android 10 - Gmail Dark
</p>
</details>

In the style block:

```html
<style>
@media (prefers-color-scheme: dark ) {
    .swap-image,
    .apple-mail-implicit-dark-support .swap-image {
      background: url('image-for-darkmode.png') no-repeat center;
      background-size: contain;
    }
     .swap-image img,
     .apple-mail-implicit-dark-support .swap-image img {
      visibility: hidden;
    }
}

[data-ogsb] .swap-image,
.apple-mail-implicit-dark-support .swap-image {
    background: url('image-for-darkmode.png') no-repeat center;
    background-size: contain;
}

[data-ogsb] .swap-image img,
    .apple-mail-implicit-dark-support .swap-image img {
    visibility: hidden;
}
</style>
```

And inline:

```html
<div class="swap-image">
    <picture>
      <source srcset="image-for-darkmode.png" media="(prefers-color-scheme: dark)">
      <img src="regular-image.png" alt="Alt Text!" width="94" height="25" border="0" style="width:94px;height:24px;color: #ffffff; font-family: Arial, sans-serif; text-align:left; font-size:28px; line-height:36px; text-decoration: none; margin: 0 auto; padding: 0;">
    </picture>
  </div>
```

## Image color inversion (hack and code from Jay Oram)

Here is another option to change image appearance in darkmode.

>This works on 
- ✔️Office 365 Dark (macOS)
- ✔️Apple mail / iOS 
	
```css
@media (prefers-color-scheme: dark) {
    .foo {
        filter: brightness(0) invert(1);
    } 
}
```

For more information, please check [Jay Oram](https://www.emailtalk.fm/episodes/08-dark-mode-w-jay-oram).

## Add a drop shadow on image

A common hack to add a white shadow around an image in dark mode

>This only works on 
- ✔️ Office 365 Dark (macOS)
- ✔️ iPhone 12 iOS 14 Dark (force dark)	

```css
@media (prefers-color-scheme: dark) {
.foo {
    filter: drop-shadow(0px 0px 10px rgba(255,255,255,0.6)) 
            drop-shadow(0px 0px 10px rgba(255,255,255,0.6))
            drop-shadow(0px 0px 10px rgba(255,255,255,0.6));
    } 
} 
```

# Keep text color on dark mode
	
## Keep text colors in dark mode (Outlook)

Following the technique described among others by Litmus, we can also easily apply it to text colors.

<details><summary>Check the support for this</summary>
<p>
**Mobile Clients**
	
| Email Clients  | Works | Don't works |
| :---         |     :---:      |     :---:      |
| iPhone Mail  |   | :x:  |
| iPad Mail  |   | :x:  |
| Gmail App (Android)  |  | :x: |
| Gmail App (iOS)  |   | :x:  |
| Outlook App (Android)  |   | :x:  |
| Outlook App (iOS)  | ✔️  |   |

**Desktop Clients**

| Email Clients  | Works | Don't works |
| :---         |     :---:      |     :---:      |
| Apple Mail | ✔️  |  |
| Outlook 2019 (Mac OS) | ✔️  |  |
| Outlook 2019 (Windows)|   | :x:  |

**Web Clients**
	
| Email Clients  | Works | Don't works |
| :---         |     :---:      |     :---:      |
| Outlook.com | ✔️  |   |
| Hey.com |   | :x: |

</p>
</details>

<details><summary>Check the support on Testi@</summary>
<p>

>This works on (testi@)

- ✔️ Office 365 Dark (macOS)
- ✔️ Android 10 - Gmail Dark
- ✔️ iPhone SE dark - Outlook
- ✔️ Outlook - Chrome (dark)

>Don't works on (testi@)

- ❌ Android 12 - Gmail Dark
- ❌ Office 365 Dark - (win)
- ❌ iPhone 12 iOS 14 (force dark)
- ❌ iPhone 12 - Gmail iOS 14 (dark) 
</p>
</details>

Add the following meta tags in order to Enable Dark Mode in email client user agents

```html
<meta name="color-scheme" content="light dark">
<meta name="supported-color-schemes" content="light dark">
```

Then add Dark Mode styles for `@media (prefers-color-scheme: dark)`:

```css
@media (prefers-color-scheme: dark ) {
    /* Custom Dark Mode Font Colors */
    h1, h2, p, span, a, b { 
        color: #ffffff !important; 
    }
}
```

Then to add support to Outlook App (Android), duplicate Dark Mode styles with `[data-ogsc]` prefix:

```css
/* Custom Dark Mode Font Colors */
[data-ogsc] h1, 
[data-ogsc] h2, 
[data-ogsc] p, 
[data-ogsc] span, 
[data-ogsc] a, 
[data-ogsc] b { 
    color: #ffffff !important; 
}
```

In your HTML:
	
```html
<p style="margin:0;color:#000000;">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. <a href="https://www.example.com" style="color: #000000;">Ut enim ad minim veniam</a>, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
```

For more information on this, please check [Litmus article](https://www.litmus.com/blog/the-ultimate-guide-to-dark-mode-for-email-marketers/) or [Jay Oram pen](https://codepen.io/emailjay/pen/BazyNdZ)

## Keep text colors in iPhone 12 iOS 14 (force dark)
	
>This works on 
- ✔️ iPhone 12 iOS 14 (force dark)
	
With the specific class described above : apple-mail-implicit-dark-support,  we can also target iPhone 12 iOs 14 (force dark) and force text color to remain the same on darkmode.
	
Example with white color : 

```css
.apple-mail-implicit-dark-support .mytitle,
.apple-mail-implicit-dark-support .subtitle {
    color:#ffffff !important;
    -webkit-text-fill-color: #ffffff !important; /* without this it doesn't work */
}
```

## MSO Gradient Solution to keep text colors in Office 365 Dark, Outlook 2021 dark, Windows 11 Mail dark (hacks and code from Nicole Merlin)

The following techniques were discovered and popularized by Nicole Merlin through the articles she wrote on Envato (link at the end of each chapter).All the code come directly from the article on the Envato website and all credits go to Envato articles. I put the reference link under each part
	
>This works on 
- ✔️ Office 365 Dark (Win)
- ✔️ Outlook 2021 (dark)
- ✔️ Windows 11 Mail (dark)

To Preserve the Color of Text in Darkmode, we can add a class to the code we want to fix. 

For example, for a white text, in the code:

```html
<p class="keep-white" style="color:#ffffff;">This text will remain WHITE</p>
```

In the style block:

```html
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

```html
<p class="keep-black" style="color:#000000;">This text will remain BLACK</p>
```

In the style block:

```html
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

For more information on this, read Nicole Merlin article: [How To Fix Outlook Dark Mode Problems (Email Design)](https://webdesign.tutsplus.com/tutorials/how-to-fix-outlook-dark-mode-problems--cms-37718)

## Keep text colors in gmail (Hack and Code from Remi Parmentier)

>This works on 
- ✔️ Gmail (iOS)
	
This technique works especially to keep white text.

```html
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

## Keep text colors in gmail (Martin Stripaj)
This trick was discovered by Martin Stripaj on [hteumeuleu email-bugs](https://github.com/hteumeuleu/email-bugs/issues/68#issuecomment-1077531703)

Explanation by Remi Parmentier: 

The idea is to force a color for Gmail using the linear-gradient trick (which Gmail doesn't change). And then on an inner element, you apply the background-clip with a forced black background and transparent text. And this gives you the text with the color applied for the background. This is very clever and a great addition to any email developer’s toolbox for dark mode.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fixing Gmail’s dark mode issue</title>
    <style>
        .body { font-size: 50px; }
        u + .body .gmail-take-this { 
            background-image:linear-gradient(#000,#000); background-clip: text; color: transparent; 
        }
    </style>
</head>
<body class="body">    
    <div style="background-image:linear-gradient(#fff4b9,#fff4b9);">
        <div class="gmail-take-this">
        This is my text
        </div>
    </div>    
</body>
</html>
```

## Force black text on dark mode in gmail (Colton Eakins)

```css
/* NEW: Force black text on dark mode. */
u + .body .gmail-blend-exclusion-blk { 
    background-color:#000; 
    mix-blend-mode:exclusion; 
}
u + .body .gmail-blend-difference-blk { 
    background-color:#000; 
    mix-blend-mode:difference; color: #fff; 
}
```

Can be used on `<span>` or `<div>`:

```html
<span class="gmail-blend-exclusion-blk"><span class="gmail-blend-difference-blk">{{YOUR_TEXT_HERE}}</span></span>
```

# Buttons
  
## Fix Buttons With a Different Colour Behind the Text in Dark Mode 

### Transparent borders

>This work on:
- ✔️ Outlook.com Webmail, 
- ✔️ Outlook for iOS, 
- ✔️ Outlook for Android

Another technique from Nicole Merlin : we can make the border transparent, e.g. `border: 8px solid transparent` so that only the background colour of the link element shows through

### Transparent background
>This work on
- ✔️ Outlook.com Webmail
- ✔️ Outlook for iOS
- ✔️ Outlook for Android

According to Nicole, we can make the <a> tag’s background transparent for Outlook only. We can do it by adding the conditional CSS to the head of the template.

For example, if the link has a class of `mylink`, we can include the following in the style block:
  
```html
<!--[if mso]>
    <style>
        .mylink {background: transparent !important;}
    </style>
<![endif]-->
```

For more information on this read Nicole Merlin article on [How to Fix Common Problems With Buttons in Dark Mode](https://webdesign.tutsplus.com/articles/fixing-problems-with-buttons-in-dark-mode-email-design--cms-39411)

### Using mso-properties

According to my test, we can get same result using `mso-shading: transparent` in the inline-style directly.

# Borders

## Fix Buttons Disappearing Into the Background in Dark Mode

>This works on 
- ✔️ Gmail App for iOS/Android
- ✔️ Outlook App for iOS/Android  
- ✔️ Outlook for Mac
- ✔️ Outlook.com
  
These email clients will keep the button dark but they will also flip the body background. This might cause issues as the button’s edges become invisible.

Here are some advices taken from Nicole's Envato article:
	
> - "Try adding a border to the outside of your button in the same colour as the background in light mode. Many email clients don’t alter CSS border colours when they process colours for Dark Mode."
>  - "Try using the CSS outline property instead of the border property if you have a square button, and you can also fake a border by nesting a button inside a slightly padded element and applying a background to that". 
>  - "By using a background image or a linear-gradient, you can actually ensure that the colour of the fake border doesn’t change."

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

## Using Media Queries to Control Borders in Dark Mode
	
>This works on
- ✔️ Apple Mail (iOS and macOS)
	
For borders, one simple Nicole advice is to force color through darkmode media queries 

```html
  <style>
    @media (prefers-color-scheme: dark) {
        .borders {
            border-color: #fafafa !important;
        }
    }
</style>
```

## Using Data Attributes to Fix Borders in Dark Mode
	
>This work on
- ✔️ outlook.com
- ✔️ Outlook Apps for iOS
- ✔️ Outlook Apps for Android

In the code
	
```html
<td class="my-border" style="border:2px solid #000000;padding:30px 40px;">
```

In the style block:
		
```html
<style>
    [data-ogsc] .my-border, 
    [data-ogsc] .my-border .btnlink {
        border: 2px solid white !important;
    }
</style>
```

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)
	
## Fix Border Problems in Outlook for Mac

>This work on
- ✔️ Outlook for Mac

> "Outlook for Mac does tend to invert border colors but it keeps dark backgrounds dark on tables and cells, but not on divs, paragraphs or link tags. So where possible, add borders to div".

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

## Fix Border Problems in Outlook for Windows

>This work on
- ✔️ Outlook for Windows

Here we can try Outlook specific code for borders, like `mso-border-alt`:
	
```
border: 2px solid #000000; mso-border-alt: 2px solid #ffffff;
```

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)
	
## Different Elements to Fix Border Problems 

Here are some other advices from Nicole, directly taken from her darkmode article.
	
#### Adjust the colors slightly 

For example, `#ffffff` to `#fafafa` or `#000000` to `#111111`.
	
#### Try Outline if You Are Working With Square Edges

>This work on
- ✔️ Windows Live Mail
- ✔️ Gmail app (iOS)
- ✔️ Microsoft365 Outlook for Windows
		
```html
<td style="outline:2px solid #ffffff;border:2px solid #000000;">
```
#### Try a Box-Shadow

>This work on
- ✔️ Apple Mail (iOS)
- ✔️ Apple Mail (macOS)
- ✔️ Outlook for Mac
		
```css
box-shadow: 0px 0px 0px 2px #ffffff;
```

or

```css
box-shadow: inset 0px 0px 0px 2px #ffffff;
```

#### Try Using CSS Blend Modes

More information on this in Nicole article [Fixing Problems With Borders in Dark Mode (Email Design)](https://webdesign.tutsplus.com/articles/fixing-problems-with-borders-in-dark-mode-email-design--cms-39410)

### MSO Gradient Solution to keep background colors in html

>This works on 
- ✔️ Office 365 Dark (Win)
	
Following Nicole's tutorial, I noticed that the mso-gradient technique also works for the background color. For example :
For a black button on outlook that becomes white in darkmode
	
```html
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

## override macOS/iOS dark mode colors

>This works on 
- ✔️ macOS/iOS
- ✔️ Outlook on Mac 

This code and text comes directly from Brian Thies on [Litmus](https://litmus.com/community/discussions/8160-ios13-dark-mode-inverting-all-colors-in-e-mail-how-to-disable#comment-16241)

For background colors, use a one color gradient:

```css
background-image: linear-gradient(#ffffff,#ffffff)
```

For text, use this along with your standard color style:

```css
-webkit-text-fill-color: #000000 !important;
```

For borders, include original border style plus...

```css
-webkit-border-before: 2px solid #000000 !important; (use for top border)
-webkit-border-after: 2px solid #000000 !important; (use for bottom border)
-webkit-border-start: 2px solid #000000 !important; (use for left border)
-webkit-border-end: 2px solid #000000 !important; (use for right border)
```

# Keep colors in VML (Nicole Merlin)

## Different Solutions to Keep text colors on VML

>This works on 
- ✔️ All Outlook that support VML

**Solution 1**

The following style attribute can be tested:

```
mso-style-textfill-fill-color:#ffffff;
```

**Solution 2**

- According to Nicole Merlin, we can use CSS positioning and z-index to layer the email content over the top of the VML content. Thus the text content remain separate from the  VML. 
- Alternatively, we can use the `mso-style-textfill-type:gradient` trick describe above
 
**Solution 3**

Use the mso style attribute: `mso-color-alt`

**In case of a White Text**
 
Nicole Merlin made some tests and found that:

- The body background must be `#555555` or lighter
- VML fill must be `#333333` or darker

Example :

```html
<body style="background-color:#555555;">
```

Or in the style block
  
```html
  <!--[if gte mso 16]>
    <style>
        body {
            background-color:#555555 !important;
        }
    </style>
<![endif]-->
```

In the <abbr title="Vector Markup Language">VML</abbr> part, we must ensure that the vml element is dark:
  
`<v:rect fillcolor="#333333">` or `<v:fill type="frame" src="image.jpg" color="#333333" />`

Then in the code:

```html
<p style="margin:0;color:#ffffff;mso-color-alt:auto;">White text</p>
```

Or we can instead use a class: 

```html
<p class="vml-white" style="margin:0;color:#ffffff;">White text</p>
```

And in the style block:

```html
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
- the body background must be `#444444` or darker
- the VML fill must be `#555555` or lighter

Example : We can put the background-color directly on a container tag:

```html
<body style="background-color:#444444;">
```

Or in the style block:

```html
  <!--[if gte mso 16]>
    <style>
        body {
            background-color:#444444 !important;
        }
    </style>
<![endif]-->
```

And in the VML shape add a dark fillcolor `<v:rect fillcolor="#555555">`

or in case of a v:fill element, add a dark color:

`<v:fill type="frame" src="image.jpg" color="#555555" />`

And in the HTML element:

```html
<p style="margin:0;color:#000000;mso-color-alt:auto;">Black text</p>
```
  
Or if we prefer, with a class on the tag:
  
```html
<p class="vml-black" style="margin:0;color:#000000;">Black text</p>
```
  
And in the style block : 

```html
<!--[if gte mso 16]>
    <style>
        .vml-black {
            mso-color-alt: auto;
        }
    </style>
<![endif]-->
```
## Transparent `<v:fill>`

On top of that, Nicole Merlin reported to me Alex Robinson's discovery which he shared on twitter:(quote) "It turns out you can keep the vml fill transparent while satisfying the light/dark fill requirement. eg `<v:rect fillcolor="#555555" opacity="0%">`" .[See the message](https://twitter.com/AlexRob22358708/status/1490879213679050752)

This is an example: We wrap the text inside a dark v:fill, and as we are giving it a dark color, we can then use `mso-color-alt:auto`, so the white text would be readable.

```html
<!--[if mso]>
  <v:rect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="website.com" style="width: 500px; height: 54px; margin-bottom: 20px; box-sizing: border-box; v-text-anchor: middle;" filled="true" strokecolor="#000000">
  <v:fill color="#555555" opacity="0"/>
    <w:anchorlock/>
    <center style="color: #000000; mso-color-alt: auto;font-family: 'GT America', Helvetica, Arial, sans-serif; font-size: 16px; font-weight: bold;">My link</center>
  </v:rect>
  <![endif]-->   
```

For more information on this read Nicole Merlin article: [Fixing Text Color Changes Inside VML](https://webdesign.tutsplus.com/tutorials/how-to-fix-outlook-dark-mode-problems--cms-37718)
