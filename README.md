# EMAIL-DARKMODE
These different techniques for dark mode were initiated by Nicole Merlin, Remi Parmentier, Mark Robbins or Annet Forcier etc, and here is a summary of all these techniques known and still functional in 2022. I will do my best to keep this page up to date, please not to point out errors or deprecated elements over time.


## Darkmode : Outlook 365 dark mode

### MSO Gradient Solution

Add a class to the code you want to fix. 
In the code :
`<p class="keep-white" style="color:#ffffff;">This text will remain WHITE</p>`
In the style :
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

## Darkmode : VML

**solution 1**
```
mso-style-textfill-fill-color:#ffffff;
```

**solution 2**

 use CSS positioning and z-index to layer your email content over the top of your VML content, keeping your text content separate from your VML. 
 use the `mso-style-textfill-type:gradient` trick
 
**solution 3**

 **If You Need White Text**
Body background must be #555555 or lighter
VML fill must be `#333333` or darker
example : 
```
<body style="background-color:#555555;">
```
  or in the style block
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
  then in the code
 ```
 <p style="margin:0;color:#ffffff;mso-color-alt:auto;">White text</p>
 ```
  
  or with a class
```
<p class="vml-white" style="margin:0;color:#ffffff;">White text</p>
```
  and in the style block
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
or in the style block
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
  

and in the html
```
<p style="margin:0;color:#000000;mso-color-alt:auto;">Black text</p>
```
  
  or with a class :
  
```
<p class="vml-black" style="margin:0;color:#000000;">Black text</p>
```
  
  and in the style block : 
```
<!--[if gte mso 16]>
    <style>
        .vml-black {
            mso-color-alt: auto;
        }
    </style>
<![endif]-->
```
  ## Buttons
  ### Fix Buttons With a Different Colour Behind the Text in Dark Mode in Outlook.com Webmail, Outlook for iOS, or Outlook for Android
  Make the border transparent, e.g. border: 8px solid transparent so that only the background colour of the link element shows through
  ## In Outlook for Windows in Dark Mode
  Make the <a> tag’s background transparent for Outlook only. You can do this by adding conditional CSS to the head of your email.

For example, if you have a link like this with a class of buttonlink: <a class="buttonlink"> you would include the following in the head of your email:
  
```
<!--[if mso]>
    <style>
        .buttonlink {background: transparent !important;}
    </style>
<![endif]-->
```
  ### Fix Buttons Disappearing Into the Background in Dark Mode in the Gmail App for iOS/Android, the Outlook App for iOS/Android, in Outlook for Mac and at Outlook.com
  These email clients will keep your button dark but flip the body background to be dark as well. Suddenly, your dark button’s edges are invisible.
  
  - Try adding a border to the outside of your button in the same colour as the background in light mode. Many email clients don’t alter CSS border colours when they process colours for Dark Mo
  - Try using the CSS outline property instead of the border property if you have a square button, and you can also fake a border by nesting a button inside a slightly padded element and applying a background to that. 
  - By using a background image or a linear-gradient, you can actually ensure that the colour of the fake border doesn’t change.
  
  
  ## Borders
  ### Using Media Queries to Control Borders in Dark Mode in Apple Mail (iOS and macOS)
	
	Example in the style block 
```
  <style>
    @media (prefers-color-scheme: dark) {
        .borders {border-color: #fafafa !important;}
    }
</style>
```

### Using Data Attributes to Fix Borders in Dark Mode in outlook.com and the Outlook Apps for iOS/Android

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
  ### Using Different Elements to Fix Border Problems in Outlook for Mac
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
  
