## css初始化文件

```css
//pc
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,form,fieldset,input,textarea,p,blockquote,th,tr,td,section,a,input,span{margin:0;padding:0; } 
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {-webkit-text-size-adjust:none;}
html,body{-webkit-user-select: none;user-select: none;-webkit-overflow-scrolling: touch;overflow-scrolling: touch;}
body,input,textarea{font-family: "Microsoft YaHei", "Simsun",Arial;-webkit-font-smoothing: antialiased;}
table {border-collapse:collapse;border-spacing:0;} 
fieldset,img {border:0} 
address,caption,cite,code,dfn,em,strong,th,var {font-style:normal;font-weight:normal} 
ol,ul {list-style:none} 
caption,th,td{text-align:center} 
h1,h2,h3,h4,h5,h6 {font-size:100%;font-weight:normal} 
q:before,q:after {content:''} 
input[type=button],button{-webkit-appearance:none;-webkit-user-select:none;}
a,input,img,select,textarea{outline: none;}
input::-webkit-search-cancel-button {display: none;}
input:focus::-webkit-input-placeholder,textarea:focus::-webkit-input-placeholder{opacity: 0;}
img{-webkit-touch-callou:none;}
.show{display:block !important;}
.hide,.none{display:none !important;}
/* clear */
.clearfix:before, .clearfix:after {content:"";display:table;}
.clearfix:after {clear:both;}
*.clearfix {zoom:1;}

//------------------------------------------------------------------------------------------





//mobile

body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,form,fieldset,input,textarea,p,blockquote,th,tr,td,section,a,input,span{margin:0;padding:0;-webkit-box-sizing:border-box;box-sizing:border-box; } 
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {-webkit-text-size-adjust:none;}
html,body{-webkit-user-select: none;user-select: none;-webkit-overflow-scrolling: touch;overflow-scrolling: touch;}
body,input,textarea{font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif,"microsoft yahei";-webkit-font-smoothing: antialiased;}
table {border-collapse:collapse;border-spacing:0;} 
fieldset,img {border:0} 
address,caption,cite,code,dfn,em,strong,th,var {font-style:normal;font-weight:normal} 
ol,ul {list-style:none} 
caption,th,td{text-align:center} 
h1,h2,h3,h4,h5,h6 {font-size:100%;font-weight:normal} 
q:before,q:after {content:''} 
input[type=button],button{-webkit-appearance:none;-webkit-user-select:none;}
a,img,input,select,li{-webkit-tap-highlight-color: rgba(0,0,0,0);}
a,img{text-decoration:none;-webkit-tap-highlight-color: rgba(0,0,0,0);-webkit-touch-callout:none;}
a,input,img,select,textarea{outline: none;}
input::-webkit-clear-button,input::-webkit-inner-spin-button,input::-webkit-outer-spin-button {-webkit-appearance: none; }
input::-webkit-search-cancel-button {display: none;}
input:focus::-webkit-input-placeholder,textarea:focus::-webkit-input-placeholder{opacity: 0;}
::-webkit-scrollbar{display:none;width: 0;}
img{-webkit-touch-callou:none;}
*{-webkit-tap-highlight-color: rgba(0,0,0,0);}
.show{display:block !important;}
.hide,.none{display:none !important;}
/* clear */
.clearfix:before, .clearfix:after {content:"";display:table;}
.clearfix:after {clear:both;}
*.clearfix {zoom:1;}
```

```css
html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
  outline: none;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html { height: 101%; }
body { font-size: 62.5%; line-height: 1; font-family: Arial, Tahoma, sans-serif; }

article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section { display: block; }
ol, ul { list-style: none; }

blockquote, q { quotes: none; }
blockquote:before, blockquote:after, q:before, q:after { content: ''; content: none; }
strong { font-weight: bold; } 

table { border-collapse: collapse; border-spacing: 0; }
img { border: 0; max-width: 100%; }

p { font-size: 1.2em; line-height: 1.0em; color: #333; }
```

```css
/*
h1-h5默认样式
*/ 
h1,h2,h3,h4,h5{
    color: #005a9c;
}
h1{
    font-size: 2.6em;
    line-height: 2.45em;
}
h2{
    font-size: 2.1em;
    line-height: 1.9em;
}
h3{
    font-size: 1.8em;
    line-height: 1.65em;
}
h4{
    font-size: 1.65em;
    line-height: 1.4em;
}
h5{
    font-size: 1.4em;
    line-height: 1.25em;
}
```