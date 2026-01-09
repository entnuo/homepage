*A modified version of [kencx's startpage](https://github.com/kencx/startpage)*

---

### Setting as the new tab page

*This was tested with Firefox 146.0. [Credits](https://old.reddit.com/r/firefox/comments/1ikvt8s/fixed_firefox_136_breaks_local_file_as_new_tab/).*

*Remember to use `sudo` when editing the following files.*

Open `/usr/lib/firefox/defaults/pref/autoconfig.js` and paste the following:

```
//
pref("general.config.filename", "mozilla.cfg");
pref("general.config.obscure_value", 0);
pref("general.config.sandbox_enabled", false);
```

Now, open `/usr/lib/firefox/autoconfig.cfg` and paste the following:

```
//  
var {classes:Cc,interfaces:Ci,utils:Cu} = Components;  

/* set new tab page */  
try {  
  ChromeUtils.defineESModuleGetters(this, {
    AboutNewTab: "resource:///modules/AboutNewTab.sys.mjs",
  }); 
  var newTabURL = "file:///<your path to index>/index.html";  
  AboutNewTab.newTabURL = newTabURL;  
} catch(e){Cu.reportError(e);} // report errors in the Browser Console
```

Restart Firefox, it should be working.
