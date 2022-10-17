# CommandHandler.java
Since I have done a lot of work on Commands, I thought I'd push a small guide on TL;DR authoring commands.

## Tl;dr
Commmands exist in a switch statement, to add a command, simply add a new entry ie: ``case "commandName":``, all commands must end in return true if it ran. If a command did not run, IE you specified if they don't have a Gold bar in their inventory -> return, still return true. When should you return false? Basically never. If you don't have a return statement in your command, it will run the NEXT command under it, which is a significant error, and should be avoided with proper encapsulation of your command.

## Decide "**who**" gets to use this command.
See the Structure of this file, open the CommandHandler class and do `CTRL+F12` to see the structure.

![img](https://i.imgur.com/QOOrHt9.png)

Which of these handlers you put the command in determines "who" can use your command. If you put the method in handleDeveloper for example, only developers can use it. In a live server, it will be disabled.

***
### Table of permissions
| Handler Method | Who can use it |
| --- | --- |
| handleRegular() | All players. |
| handleSupport() | All support & higher ranking staff. |
| handleTrialMod() | All trial mods & higher ranking staff. AKA tier 1 mods. |
| handleQualifiedMod() | All qualified mods & higher ranking staff. AKA Tier 2 mods. |
| handlePaidMod() | All paid mods & higher ranking staff. AKA Tier 3 mods. |
| handleAdmin() | All administrators and owners. |
| handleDeveloper() | **ONLY Admins in an OfflineMode, Dev server.** |

### Example: 
* You create a command in handleAdmin(), it can be used by devs and admins will be able to use it in the live server.
* You create a command in handleDeveloper(), it can be used by devs and will NOT work in the live server.
* You create a command in handleTrialMod(), it can be used by Trial Mods, Qualified Mods, Paid Mods, Admins & Devs. Because higher-ranking staff can always access lower-ranking commands.

## Decide "**what**" the command does.
The best way to see how commands work is to view an existing command. You can see "empty" for a simple example:
```
            case "empty": {
                player.getInventory().clear();
                return true;
            }
```
Note: There's a case, it does something, and there's a return. If I could give 1 critique, it would be it does not send a message to the user. It's always good to provide feedback to the user so a simple message stating their items have been emptied would suffice. 

![img](https://i.imgur.com/YKbqDL9.png)

Much better.
