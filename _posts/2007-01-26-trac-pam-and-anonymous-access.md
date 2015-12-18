---
id: 154
title: Trac, PAM, and Anonymous Access
author: Wyatt
excerpt: Recently at HTG, we had the need to have anonymous access to create Trac tickets, but still maintain authentication to the other areas of Trac.
layout: post
guid: http://blog.hackerforhire.org/?p=154
permalink: /2007/01/26/trac-pam-and-anonymous-access/
autometa:
  - trac trac pythonoption authentication anonymous tracenvparentdir pythondebug pythonpath
categories:
  - Technology
---
Recently at HTG, we had the need to have anonymous access to create Trac tickets. This is all well and good if you are using Trac with it&#8217;s own built in authentication; however, it gets a little more hairy when you are trying to use PAM for authentication. The big gain from PAM is that our developers only need 1 password for login to the box, login to SVN, and login to Trac. I could have figured this out a lot sooner if I&#8217;d read the documentation better; however, that&#8217;s not a typical engineer/hacker attitude. Also, this wasn&#8217;t able to be found by Google because so many people have &#8220;provided by &#8216;Trac'&#8221; in their pages that sifting just took forever. Anyway, here&#8217;s our setup for PAM authentication (this goes in your **location /projects** tag):

<div class="codesnip-container" >
  <div class="apache codesnip">
    <<span class="kw3">location</span> /projects><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">SetHandler</span> mod_python<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonHandler trac.web.modpython_frontend<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracEnvParentDir /opt/trac<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracUriRoot <span class="st0">"/projects"</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonDebug <span class="kw2">on</span></p> 
    
    <p>
      &nbsp; &nbsp; &nbsp; &nbsp; PythonPath <span class="st0">"sys.path + [&#8216;/opt/trac&#8217;]"</span>
    </p>
    
    <p>
      &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">AuthType</span> Basic<br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">AuthName</span> <span class="st0">"Dev"</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; AuthPAM_Enabled <span class="kw2">on</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">Require</span> <span class="kw1">group</span> admin<br /> </<span class="kw3">location</span>></div> </div> 
      
      <p>
        Pretty simple, just sets up our generic stuff. This is what I had to add to change it to get anonymous authentication AND HTTP basic auth when you click the little login button (our Trac is setup so anonymous can read the how-to&#8217;s in the wiki, but nothing else).
      </p>
      
      <div class="codesnip-container" >
        <div class="apache codesnip">
          <<span class="kw3">location</span> /projects><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">SetHandler</span> mod_python<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonHandler trac.web.modpython_frontend<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracEnvParentDir /opt/trac<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracUriRoot <span class="st0">"/projects"</span></p> 
          
          <p>
            &nbsp; &nbsp; &nbsp; &nbsp; PythonPath <span class="st0">"sys.path + [&#8216;/opt/trac&#8217;]"</span>
          </p>
          
          <p>
            <span class="co1"># &nbsp; &nbsp; &nbsp; AuthType Basic</span><br /> <span class="co1"># &nbsp; &nbsp; &nbsp; AuthName "Dev"</span><br /> <span class="co1"># &nbsp; &nbsp; &nbsp; AuthPAM_Enabled on</span><br /> <span class="co1"># &nbsp; &nbsp; &nbsp; Require group admin</span><br /> </<span class="kw3">location</span>>
          </p>
          
          <p>
            <<span class="kw3">location</span> /projects/*/login>;<br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="kw1">SetHandler</span> mod_python<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonHandler trac.web.modpython_frontend<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracEnvParentDir /opt/trac<br /> &nbsp; &nbsp; &nbsp; &nbsp; PythonOption TracUriRoot <span class="st0">"/projects"</span>
          </p>
          
          <p>
            &nbsp; &nbsp; &nbsp; &nbsp; PythonPath <span class="st0">"sys.path + [&#8216;/opt/trac&#8217;]"</span>
          </p>
          
          <p>
            &nbsp; &nbsp; &nbsp; &nbsp;<span class="kw1">AuthType</span> Basic<br /> &nbsp; &nbsp; &nbsp; &nbsp;<span class="kw1">AuthName</span> <span class="st0">"Dev"</span><br /> &nbsp; &nbsp; &nbsp; &nbsp;AuthPAM_Enabled <span class="kw2">on</span><br /> &nbsp; &nbsp; &nbsp; &nbsp;<span class="kw1">Require</span> <span class="kw1">group</span> admin<br /> </<span class="kw3">location</span>></div> </div> 
            
            <p>
              There is probably some repeat stuff in there; but it doesn&#8217;t seem to break things. Hope this helps someone else out there looking to do the same thing. As a side note, this is not generally a good idea since your are sending basic auth (i.e. plain text) login info over unencrypted connections.
            </p>
            
            <p>
              <strong>Update:</strong>Stupid WordPress wasn&#8217;t auto-escaping the code correctly, if you view it now, you should be able to see the location tags used in the apache configuration.
            </p>