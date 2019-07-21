
## DEFENSE AGAINST THE DARK ARTS
### CS373 - SUMMER 2019
<br>
[Week 2](index.md)  [Week 3](week3.md)

<br><br>
## Week 4 Write-Up:  Software Vulnerabilities and Exploits

### Using WinDBG

Using WinDBG, a standard debugging tool, we can view assembly level processes occuring while running a malicious executable. Since there has been an increase in browser based attacks over the past several years, we will examine code that attempts to exploit website and browser based vulnerabilities.

Once FSExplorer.html is open and we allow scripts to be run, we attach the tab process (second process to be executed when launching Internet Explorer) in WinDBG, set a breakpoint, and allow the code to execute till we reach the breakpoint. From here, we can view where the module is loaded in memory using the lm or lmf command in WinDGB. FSExploitMe is loaded at 54430000. We can also determine stack size, starting address of heap, view register values, determine amount of space allocated for local variables on the stack, view string values on the stack, view different formats of values, and lots more.

![Answer1](FSExploitMe_1.JPG)
![Answer2](FSExploitMe_2.JPG)
![Answer3](FSExploitMe_3.JPG)
![Answer4](FSExploitMe_4.JPG)
![Answer5](FSExploitMe_5.JPG)
![Answer6](FSExploitMe_6.JPG)
![Answer7](FSExploitMe_7.JPG)
![Answer8](FSExploitMe_8.JPG)
![Answer9](FSExploitMe_9.JPG)
<br>

Go [here](http://windbg.info/doc/1-common-cmds.html) to see a list of common WinDBG commands.

Go [here](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/x86-architecture) to learn about x86 architecture, including how the internal registers are used.


### References
Antoniewicz, Brad, Foundstone, *Vulnerabilities and Expoits*, OSU CS-373 DEFENSE AGAINST THE DARK ARTS

