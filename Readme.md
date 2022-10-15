# Theme loader script
## By pyroclasticDusk

### V4 minified
`javascript:d=window.parent.document;function m(t){for(e in t)q(':root').style.setProperty(e,t[e]);r=t.songURL,n=t.songName,i=~~(Math.random()*r.length),(o=q('.songName a')).innerHTML=n[i],o.href=q('#songAudio').src=r[i]}function g(){u=w+this.title,q('#current').innerHTML=this.firstChild.textContent,fetch(u).then(t=>t.json()).then(t=>{m(t)}).catch(t=>{throw t})}function b(){u=w+this.title,v=k.bind(this),fetch(u).then(t=>t.json()).then(t=>{v(t,this)}).catch(t=>{throw t})}function k(t,s){for(i=0;i<p.length;i++)s.style.setProperty(p[i],t[p[i]]);s.querySelector('.themeicon').style.setProperty('background-image',t['--image'])}for(j=0,w='https://raw.githubusercontent.com/evynumberfour/themes/main/data/',q=d.querySelector.bind(d),l=d.getElementsByClassName('theme'),p=['--border','--hoverborder','--themelink','--textshadowsecondary','--primary'];j<l.length;j++)l[j].addEventListener('click',g),l[j].style.cursor='pointer',l[j].style.opacity=1,(y=b.bind(l[j]))();console.log('running');`

### V4 Expanded and notated
```javascript
javascript:
let doc = window.parent.document, 
    // grabs shorthand for parent document NOTE1
    
    query = doc.querySelector.bind(doc), 
    // shorthand for finding elements by css tags
    
    domain = 'https://raw.githubusercontent.com/evynumberfour/themes/main/data/', 
    // the domain under which your files are hosted, used to reduce redundant html 
    
    properties = ['--border', '--hoverborder', '--themelink', '--textshadowsecondary', '--primary'] 
    // list properties to be applied to library item theme element
    
    themeclass = 'theme'; 
    // the css class which all theme link elements share 
    
function implement(theme) { // self explanatory

  let root = query(':root'); 
  for (property in theme) {root.style.setProperty(property, theme[property]); 
  // grab css root and transfer all theme properties onto it
  
  let songArray = theme.songURL; 
  let songNames = theme.songName;
  // store music related properties
  
  i = ~~(Math.random() * songArray.length); 
  //convert random number within songArray range to integer using two binary NOT operators 
  
  songNameElement=query('.songName a');
  songNameElement.innerHTML=songNames[i];
  songNameElement.href = query('#songAudio').src = songArray[i];
  // replace the displayed song with the randomly selected one
  
}

function jsonGetter() { // used to communicate with offsite file hosting

  url = domain + this.title; 
  fetch(url).then(
    rawfile => rawfile.json();
  ).then(
    jsonoutput => {implement(jsonoutput)}
  ).catch(
    error => {throw error}
  )
  // gets theme url, grabs data from said url, converts to json and feeds to implementor function 
  // (and catches any http errors)
  
  q('#current').innerHTML = this.firstChild.textContent; 
  // replace current theme name with the name of the selected theme
  
}
  
function jsonGetterForLI() {

  url = domain + this.title;
  
  let boundLIimplimentor = LIimplement.bind(this);
  // create function with same context of this function, ie the theme link element
  
  fetch(url).then(
    rawfile => rawfile.json();
  ).then(
    jsonoutput => {boundLIimplementor(jsonoutput, this)}
  ).catch(
    error => {throw error}
  )
  // same as normal jsongetter, but doesnt change name of current theme, 
  // and feeds json output to other theme-link-element-specific implementor
}

function LIimplement(theme, libraryItem) {

  for (i = 0; i < properties.length; i++) {
  
    libraryItem.style.setProperty(properties[i], theme[properties[i]]);
    // apply all specified properties to the theme link element
  
  } 
  
  libraryItem.querySelector('.themeicon').style.setProperty('background-image', theme['--image'])
  // set the theme icon
  
}
  
let themelist = doc.getElementsByClassName(themeclass); // get all theme elements from set class

for (i = 0; i < l.length; i++) {

  let themeblock = themelist[i];
  // grab the current iterated theme link element
  
  themeblock.addEventListener('click', jsonGetter);
  // add event listener to grab its theme and implement it on click
  
  themeblock.style.cursor = 'pointer';
  themeblock.style.opacity = 1;
  // remove the "disabled" appearance
  
  (function() { 
    jsonGetterForLibraryItems.bind(themelist[i]) 
  })();
  // create an anonymous function bound to the themelink that implements its theme on itself
  
}

console.log('running');

```
[1]: Also attempts to grab higher window context, but this either defaults to the current window context or is blocked by basic iframe security
