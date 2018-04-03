# Week 8 Assignment

## Vulnerability #1
Green Target displays if login exists in database with **bold**

![Green existing](https://i.imgur.com/ZGnh7CT.png)
![Green nonexisting](https://i.imgur.com/9aE3yFF.png)

- Meanwhile, it doesn't happen to red or blue and they display both existing and nonexisting logins equally
![Red existing](https://i.imgur.com/XIoHpKX.png)
![Red nonexisting](https://i.imgur.com/WHO8ckL.png)

**Conclusion:** 

We can brute force jmornoe's username by simply adding a digit to the back and Green target will inform us if certain login exists or not.

## Vulnerability #2
Blue, Red and Green Targets are affected by this exploit

- Add A State to a Country with `<script>alert('Daulet found the XSS!');</script>` as name and position
- Add Territory to the State with the same values

![BlueRedGreen XSS](https://i.imgur.com/iqabtms.png)
