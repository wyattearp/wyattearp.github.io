---
id: 166
title: SWFUpload and Dynamic POST
author: Wyatt
layout: page
guid: http://blog.hackerforhire.org/swfupload-and-dynamic-post/
autometa:
  - swfupload upload currentfile dynamically upload_script string uploadscriptisfunction caption
---
Recently, it came across the need to generate the upload_script string dynamically. This can be useful if you are trying to pass additional arguement along with the file such as a caption that is different for each file. I figured I&#8217;d drop it here so maybe someone else who is in the same boat doesn&#8217;t have to have such a hard learning curve <img src="http://blog.hackerforhire.org/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

First, we define a callback function that dynamically generates our upload string:

<div class="codesnip-container" >
  <div class="javascript codesnip">
    <span class="kw2">function</span> generateUploadString <span class="br0">&#40;</span>file<span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw2">var</span> basestring <span class="sy0">=</span> <span class="st0">&#8216;/rem/upload/uploadFile?&#8217;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw2">var</span> cookie <span class="sy0">=</span> readCookie<span class="br0">&#40;</span><span class="st0">&#8216;JSESSIONID&#8217;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw2">var</span> caption <span class="sy0">=</span> <span class="st0">&#8216;&caption=&#8217;</span> <span class="sy0">+</span> document.<span class="me1">getElementById</span><span class="br0">&#40;</span>file.<span class="me1">id</span><span class="sy0">+</span><span class="st0">&#8216;caption&#8217;</span><span class="br0">&#41;</span>.<span class="me1">value</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">return</span> dwrString<span class="sy0">+</span>cookie<span class="sy0">+</span>caption<span class="sy0">;</span><br /> <span class="br0">&#125;</span>
  </div>
</div>

I should note when I generated my file\_queue lines that i added an input field with the file.id+caption as its identifier. Next, we need to edit the SWFUpload-src.js file and add a field to tell if the upload\_script variable is function or a string

<div class="codesnip-container" >
  <div class="javascript codesnip">
    &#8230;&#8230;.<br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">this</span>.<span class="me1">addSetting</span><span class="br0">&#40;</span><span class="st0">"flash_target"</span><span class="sy0">,</span> settings<span class="br0">&#91;</span><span class="st0">"flash_target"</span><span class="br0">&#93;</span><span class="sy0">,</span> <span class="st0">""</span><span class="br0">&#41;</span><span class="sy0">;</span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">// Where to output the flash (not used)</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">this</span>.<span class="me1">addSetting</span><span class="br0">&#40;</span><span class="st0">"flash_width"</span><span class="sy0">,</span> settings<span class="br0">&#91;</span><span class="st0">"flash_width"</span><span class="br0">&#93;</span><span class="sy0">,</span> <span class="st0">"1px"</span><span class="br0">&#41;</span><span class="sy0">;</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">// Flash width</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">this</span>.<span class="me1">addSetting</span><span class="br0">&#40;</span><span class="st0">"flash_height"</span><span class="sy0">,</span> settings<span class="br0">&#91;</span><span class="st0">"flash_height"</span><span class="br0">&#93;</span><span class="sy0">,</span> <span class="st0">"1px"</span><span class="br0">&#41;</span><span class="sy0">;</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">// Flash height</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">this</span>.<span class="me1">addSetting</span><span class="br0">&#40;</span><span class="st0">"flash_color"</span><span class="sy0">,</span> settings<span class="br0">&#91;</span><span class="st0">"flash_color"</span><span class="br0">&#93;</span><span class="sy0">,</span> <span class="st0">"#000000"</span><span class="br0">&#41;</span><span class="sy0">;</span> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">// Flash color</span></p> 
    
    <p>
      &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//dynamic generation of upload_script variable</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">this</span>.<span class="me1">addSetting</span><span class="br0">&#40;</span><span class="st0">&#8216;upload_script_is_function&#8217;</span><span class="sy0">,</span> settings<span class="br0">&#91;</span><span class="st0">&#8216;upload_script_is_function&#8217;</span><span class="br0">&#93;</span><span class="sy0">,</span> <span class="st0">&#8221;</span><span class="br0">&#41;</span><span class="sy0">;</span>
    </p>
    
    <p>
      &nbsp; &nbsp; &nbsp; &nbsp;&#8230;..<br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="me1">sb</span>.<span class="me1">append</span><span class="br0">&#40;</span><span class="st0">"&uploadQueueCompleteCallback="</span> <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">getSetting</span><span class="br0">&#40;</span><span class="st0">"upload_queue_complete_callback"</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; sb.<span class="me1">append</span><span class="br0">&#40;</span><span class="st0">"&autoUpload="</span> <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">getSetting</span><span class="br0">&#40;</span><span class="st0">"auto_upload"</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; sb.<span class="me1">append</span><span class="br0">&#40;</span><span class="st0">"&allowedFiletypes="</span> <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">getSetting</span><span class="br0">&#40;</span><span class="st0">"allowed_filetypes"</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; sb.<span class="me1">append</span><span class="br0">&#40;</span><span class="st0">"&maximumFilesize="</span> <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">getSetting</span><span class="br0">&#40;</span><span class="st0">"allowed_filesize"</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; sb.<span class="me1">append</span><span class="br0">&#40;</span><span class="st0">"&uploadScriptIsFunction="</span> <span class="sy0">+</span> <span class="kw1">this</span>.<span class="me1">getSetting</span><span class="br0">&#40;</span><span class="st0">&#8216;upload_script_is_function&#8217;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &#8230;..</div> </div> 
      
      <p>
        Now we need to actually modifiy the SWFUpload action script and add the uploadScriptIsFunction variable:
      </p>
      
      <div class="codesnip-container" >
        <div class="actionscript codesnip">
          &#8230;..<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="me1">uploadQueueCompleteCallback</span> = <span class="kw3">_root</span>.<span class="me1">uploadQueueCompleteCallback</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; flashLoadedCallback = <span class="kw3">_root</span>.<span class="me1">flashLoadedCallback</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; uploadFileStartCallback = <span class="kw3">_root</span>.<span class="me1">uploadFileStartCallback</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; uploadScriptIsFunction = <span class="kw3">_root</span>.<span class="me1">uploadScriptIsFunction</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &#8230;&#8230;
        </div>
      </div>
      
      <p>
        And our modification to the upload() function:
      </p>
      
      <div class="codesnip-container" >
        <div class="actionscript codesnip">
          <span class="co1">// Start upload</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">if</span><span class="br0">&#40;</span>uploadScriptIsFunction<span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//user says this is dynamically generated</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; currentFile.<span class="me1">upload</span><span class="br0">&#40;</span><span class="kw3">String</span><span class="br0">&#40;</span>ExternalInterface.<span class="kw3">call</span><span class="br0">&#40;</span>uploadScript, getFileObject<span class="br0">&#40;</span>currentFileId, currentFile<span class="br0">&#41;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="br0">&#41;</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="br0">&#125;</span> <span class="kw1">else</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//statically specified</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; currentFile.<span class="me1">upload</span><span class="br0">&#40;</span>uploadScript<span class="br0">&#41;</span>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <span class="br0">&#125;</span>
        </div>
      </div>
      
      <p>
        Now when you create your SWFUpload object in Javascript, just specify it like such to take advantage of the new feature:
      </p>
      
      <div class="codesnip-container" >
        <div class="javascript codesnip">
          swfu <span class="sy0">=</span> <span class="kw2">new</span> SWFUpload<span class="br0">&#40;</span><span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; upload_script<span class="sy0">:</span> <span class="st0">&#8216;generateUploadString&#8217;</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; upload_script_is_function<span class="sy0">:</span> <span class="kw2">true</span><span class="sy0">,</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &#8230;&#8230;.
        </div>
      </div>
      
      <p>
        Oh yeah, and we have to rebuild the flash app to, so for me that&#8217;s:
      </p>
      
      <div class="codesnip-container" >
        <div class="bash codesnip">
          mtasc classes<span class="sy0">/</span>com<span class="sy0">/</span>mammon<span class="sy0">/</span>swfupload<span class="sy0">/*</span>.as <span class="re5">-swf</span> SWFUpload.swf <span class="re5">-version</span> <span class="nu0">8</span> <span class="re5">-main</span> <span class="re5">-v</span> <span class="re5">-header</span> <span class="nu0">1</span>:<span class="nu0">1</span>:<span class="nu0">12</span>:FFFFFF
        </div>
      </div>
      
      <p>
        Hope it helps someone.
      </p>