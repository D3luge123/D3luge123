- DOM based Cross Site Scripting found in http://www.testfire.net

Summary:

The website that is known as http://www.testfire.com was found to contain a critical vulnerability called as DOM based Cross Site Scripting, which is a type of Javascript vulnerability. According to Wikipedia, Cross site scripting or XSS attacks allow attackers to inject client-site scripts into web pages viewed by other users. They may be used to access bypass controls.DOM based XSS vulnerabilities usually occur when Javascript takes data from an attacker controllable source, such as URL and passes it to a sink that supports Dynamic code execution, such as eval() or innerHTML.When an attacker gets a user's browser to execute his/her code, the code will run within the security context (or zone) of the hosting web site. With this level of privilege, the code has the ability to read, modify and transmit any sensitive data accessible by the browser. A Cross-site Scripted user could have his/her account hijacked (cookie theft), their browser redirected to another location, or possibly shown fraudulent content delivered by the web site they are visiting. Cross-site Scripting attacks essentially compromise the trust relationship between a user and the web site. Applications utilizing browser object instances which load content from the file system may execute code under the local machine zone allowing for system compromise.


Payload used:

                  ?name=abc#<img src="random.gif" onerror=alert(5397)>    
![Screenshot_2022-03-09_16_09_07](https://user-images.githubusercontent.com/101284893/157538188-b7317fe8-9b94-446f-9f4d-34c9cc7c1ff9.png)
![Screenshot_2022-03-09_16_19_29](https://user-images.githubusercontent.com/101284893/157538194-3a636a67-e572-411f-a968-fa37a166f93f.png)



Steps to reproduce:

To reproduce this vulnerability:

1)A Javascript payload needs to be generated for the victim to execute it. A simple payload can be generated by using the document.write sink as follows : ?name=abc#<img src="random.gif" onerror=alert(5397)>

2)This Javascript code should be injected properly into the vulnerable parameter. The code should look like the following:

    GET http://www.testfire.net/admin HTTP/1.1
    Host: www.testfire.net
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:92.0) Gecko/20100101 Firefox/92.0
    Pragma: no-cache
    Cache-Control: no-cache
    Referer: http://www.testfire.net/index.jsp?content=personal_other.htm
    Cookie: JSESSIONID=72AB73DB822E3625547D5115EB0F6C77
![Screenshot_2022-03-09_13_45_14](https://user-images.githubusercontent.com/101284893/157511075-98cab3c1-22cb-466d-992b-9d19214b3df2.png)

3) As this injection happens in a GET parameter, the attacker now simply needs to send the crafted link that produces the GET request and have the victim click on it.

Impact :
XSS can cause serious issues. Attackers often leverage XSS to steal session cookies and impersonate the user. Attackers can also use XSS to deface websites, spread malware, phish for user credentials, support social engineering techniques, and many more.User accounts can be hijacked, credentials could be stolen, sensitive data could be exfiltrated, and lastly, access to your client computers can be obtained.Various research and studies identified that up to 50% of websites are vulnerable to DOM-based XSS vulnerabilities.

Prevention of DOM XSS:
The primary rule that a user must follow to prevent DOM XSS is to sanitize all untrusted data, even if it is only used in client-side scripts. If the user has to use user input on the page, they should always use it in the text context, never as HTML tags or any other potential code.

Avoid methods such as document.innerHTML and instead use safer functions, for example, document.innerText and document.textContent.The user can entirely avoid using user input, especially if it affects DOM elements such as the document.url, the document.location, or the document.referrer.
