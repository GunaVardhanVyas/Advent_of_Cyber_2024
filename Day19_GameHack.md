# Day 19[Game_Hacking]: I merely noticed you're improperly stored, my dear secret!

## Story :
Glitch is onto Mayor Malware and he sure is about to discover something in the mayors secret lait downtown, when glitch dicovers that the door is locked and the key is inside a game. Why? because the mayor thought 'no one can hack a game'. (Comical, i know...the first thing the comes to mind when i hear hacking is video game hacking and cheating.)

## Learning Objectives : 
- Understand how to interact with an executable's API.
- Intercept and modify internal APIs using Frida.
- Hack a game with the help of Frida.

## Abbreviations and Applications :
- [API](https://aws.amazon.com/what-is/api/) : Application Programme Interface, is a set of rules and protocols for building software and applications.
- [Frida](https://frida.re/) : Dynamic instrumentation toolkit for developers, reverse-engineers, and security researchers.

## Process Key Steps and Points :
- Hacking a game can be pretty complex since it requires different skills, including memory management, reverse engineering, and networking knowledge if the game runs online.
- Frida creates a thread in the target process; that thread will execute some bootstrap code that allows the interaction. This interaction, known as the agent, permits the injection of JavaScript code, controlling the application's behaviour in real-time. And this is how we can analyze, modify and interact with the running applications.
- The **Interceptor** : crucial functionality of Frida that lets us alter internal functions' input or output or observe their behaviour.
- `frida-trace` to create handlers for libraries used by the application. Each handler has two functions called `hooks` :
  - **onEnter** : we are mainly interested in the *args* variable, an array of pointers to the parameters used by our target function.
  - **onLeave** :  we are interested in the *retval* variable. (contains pointer to returned variable)
  
## Tools and Commands Used :
- `frida-trace ./app -i '*'` : Created handlers for all the libraries used by the application 'app'.
  
## Questions, Hints and Answers :
1. What is the OTP flag?
   - Hint : use `arg[0]` in the function handler `_Z7set_otpi()` in `onEnter` hook.
   - ![param](/Screenshots/D19Q1a.png)
   - ![OTPFlag](/Screenshots/D19Q1.png)
   - Ans : `THM{one_tough_password}`
2. What is the billionaire item flag?
   - Hint : use `arg[1] = ptr(0)` in the function handler `_Z17validate_purchaseiii()` in `onEnter` Hook.
   - ![billItemFlag](/Screenshots/D19Q2.png)
   - Ans : `THM{credit_card_undeclined}`
3. What is the biometric flag?
   - Hint : use `retval.replace(ptr(1))` to make the flag true in `onLeave` hook of `_Z16check_biometricsPKc()` handler.
   - ![bioFlag](/Screenshots/D19Q3.png)
   - Ans : `THM{dont_smash_your_keyboard}`
