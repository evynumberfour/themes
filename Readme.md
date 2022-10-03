# Theme loader script
## By pyroclasticDusk

### V4 minified
`javascript:d=window.parent.document;function m(t){for(e in t)q(':root').style.setProperty(e,t[e]);r=t.songURL,n=t.songName,i=~~(Math.random()*r.length),(o=q('.songName a')).innerHTML=n[i],o.href=q('#songAudio').src=r[i]}function g(){u=w+this.title,q('#current').innerHTML=this.firstChild.textContent,fetch(u).then(t=>t.json()).then(t=>{m(t)}).catch(t=>{throw t})}function b(){u=w+this.title,v=k.bind(this),fetch(u).then(t=>t.json()).then(t=>{v(t,this)}).catch(t=>{throw t})}function k(t,s){for(i=0;i<p.length;i++)s.style.setProperty(p[i],t[p[i]]);s.querySelector('.themeicon').style.setProperty('background-image',t['--image'])}for(j=0,w='https://raw.githubusercontent.com/evynumberfour/themes/main/data/',q=d.querySelector.bind(d),l=d.getElementsByClassName('theme'),p=['--border','--hoverborder','--themelink','--textshadowsecondary','--primary'];j<l.length;j++)l[j].addEventListener('click',g),l[j].style.cursor='pointer',l[j].style.opacity=1,(y=b.bind(l[j]))();console.log('running');`

### V4 Expanded and notated
```javascript
javascript:
let doc = window.parent.document, // grabs shorthand for parent document NOTE1
    query = doc.querySelector.bind(doc), // shorthand for finding elements by css tags
    domain = 'https://raw.githubusercontent.com/evynumberfour/themes/main/data/', // the domain under which your files are hosted, used to reduce redundant html 
    themelist = doc.getElementsByClassName('theme'), // get all theme elements
    properties = ['--border','--hoverborder','--themelink','--textshadowsecondary','--primary']; // list properties to be applied to library item theme element
    
function implement(theme) { // self explanatory

  let root = query(':root'); 
  for(property in theme) {root.style.setProperty(property,theme[property]); 
  // grab css root and transfer all theme properties onto it
  
  let songArray = theme.songURL; 
  let songNames = theme.songName;
  // store music related properties
  
  i = ~~(Math.random() * songArray.length); //convert random number within songArray range to integer using two binary NOT operators 
  
  songNameElement=query('.songName a');
  songNameElement.innerHTML=songNames[i];
  songNameElement.href = query('#songAudio').src = songArray[i];
  // replace the displayed song with the randomly selected one
  
}

function jsonGetter() { // used to communicate with offsite file hosting

  url = domain + this.title; 
  fetch(url).then(rawfile => rawfile.json()).then(jsonoutput => {implement(jsonoutput)}).catch(error => {throw error})
  // get theme url, grab data from said url, convert to json and feed to implementor function, and catches and http errors. 
  
  q('#current').innerHTML = this.firstChild.textContent; 
  // replace current theme name with selected
  
}
  
function jsonGetterForLI() {

  url = domain + this.title;
  boundLIimplimentor = LIimplement.bind(this);
  fetch(url).then(rawfile => rawfile.json()).then(jsonoutput => {boundLIimplementor(jsonoutput, this)}).catch(error => {throw error})
  
}
function LIimplement(theme, libraryItem) {
  for (i=0; i<properties.length; i++) {
    libraryItem.style.setProperty(properties[i],theme[properties[i]]);
  }
  libraryItem.querySelector('.themeicon').style.setProperty('background-image',theme['--image'])
}
  
for (i=0; i<l.length; i++) {
  themelist[i].addEventListener('click',jsonGetter);
  themelist[i].style.cursor = 'pointer';
  themelist[i].style.opacity = 1;
  (y=jsonGetterForLibraryItems.bind(l[j]))();
}
console.log('running');
```
[1]: Also attempts to grab higher window context, but this either defaults to the current window context or is blocked by basic iframe security
