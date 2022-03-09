Reflected Cross Site Scripting found in http://testasp.vulnweb.com/

Summary: 

Reflected cross-site scripting arises when an application receives data in an HTTP request and then includes that data within the immediate response in an unsafe way.The script is activated through a link, which then sends a request to a website with a vulnerability that enables execution of malicious scripts.An example of reflected cross-site scripting is a search form, where visitors send their search query to the server and only they see the result.The code itself is mostly written in HTML/JavaScript, but may also extend to VBScript, ActiveX, Java, Flash, and many more.Examples of an attacker's favorite targets include message board posts, web mail messages, and web chat software. The unsuspecting user is not required to interact with any additional site/link and just simply view the web page containing the code.

Vulnerability used: 

        <script>alert(1)</script>
        
 ![Screenshot_2022-03-09_16_49_36](https://user-images.githubusercontent.com/101284893/157544853-da092b03-9c5e-480f-8e66-ae281e9a9374.png)



Steps to reproduce:
1)The first step to inject the payload is by visiting the site http://testasp.vulnweb.com/

2)The attacker now simply needs to go to the search section on the site and inject a simple payload <script>alert(1)</script> on the search bar. 

3)The injected Javascript must look like the following:

    GET http://testasp.vulnweb.com/Search.asp?tfSearch=%22%3E%3CscrIpt%3Ealert%281%29%3B%3C%2FscRipt%3E HTTP/1.1
    Host: testasp.vulnweb.com
    User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    Accept-Language: en-US,en;q=0.5
    Connection: keep-alive
    Referer: http://testasp.vulnweb.com/Search.asp
    Cookie: ASPSESSIONIDASRBTARC=BIJGNNHAIBAHACODDOGNOJDC
    Upgrade-Insecure-Requests: 1
    Content-Length: 0
    
 ![Screenshot_2022-03-09_16_50_38](https://user-images.githubusercontent.com/101284893/157544471-b8c0bb09-2e08-4c9b-bbaf-36277c3891fd.png)
![Screenshot_2022-03-09_16_51_15](https://user-images.githubusercontent.com/101284893/157544472-d15bc8e2-6d75-4f6c-bcf2-d38a398bbb6b.png)


4)This will trigger the vulnerability from the Attacker's side. Now he simply needs to wait for the user to prompt the GET request.

Impact:
If an attacker can control a script that is executed in the victim's browser, then they can fully compromise that user.It ranges from session hijacking to credential theft and many more. By exploiting a cross-site scripting vulnerability, an attacker can easily impersonate a legitimate user and hence take over their account.Amongst many other things, the attacker can:

    Easily perform any action within the application that the user can perform.
    View any information that the user is able to view.
    Modify any type of information that the user is able to modify.
    Initiate interactions with other application users that will appear to originate from the initial victim user.
    
    Prevention of Reflected XSS:
    
    First and foremost, vigilance is the best way to avoid XSS scripting. Specifically, this means not clicking on malicious links which may contain malicious coding. Suspicious links include those found in:

    Emails from unknown senders
    A website’s comments section
    Social media feed of unknown users,etc
    
    Additionally, web application firewalls (WAFs) also play an important role in mitigating reflected XSS attacks. 
    
    Video Source:
    

https://user-images.githubusercontent.com/101284893/157544556-1582f1b7-be67-40b8-9cd8-0b68b8d36c56.mp4



https://user-images.githubusercontent.com/101284893/157544562-043aa41c-eea6-455a-93ee-e701755231f0.mp4



    
    
