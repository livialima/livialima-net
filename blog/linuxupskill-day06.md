# Day 6 : Vim Crash Course

This is part of the [#LinuxUpSkillChallenge](../challenges/linux-upskill.html). Don't forget to also check out the [Official Instructions](https://github.com/snori74/linuxupskillchallenge/blob/master/06.md) and the [Reddit](https://www.reddit.com/r/linuxupskillchallenge/) posts.

*video*

## Objectives of the day
1. **Dealing with files**

```vim filename``` - create/open file

```:w``` - save

```:w newfilename``` - save as

```:q!``` - close file and trash all changes (the ```!``` forces the command)

```:wq``` - save and close

2. **Navigation**

![](../img/vim-hjkl.png)

```gg``` - BOF

```G``` - EOF

3. **Vim modes:** Normal, Insert, Visual, Command. Check out the [freecodecamp post](https://www.freecodecamp.org/news/vim-editor-modes-explained/) for more details.

4. **Editing**

```d``` - Cut (delete)

```y``` - Copy (yank)

```p``` - Paste

```u``` to undo the last command

```CRTL + R``` - Redo

```/``` - Find

```:%s/old/new/gc``` - Replace all occurrences of ```old``` for ```new```, globally inside the file, and prompt a confirmation for every replacement

4. To learn more, please check:

```vimtutor``` - VIM own tutorial

[VIM Adventures](https://vim-adventures.com/)

[VimScript on exercism.io](https://exercism.io/my/tracks/vimscript)

For more detail on how I did each day, check out my log on [Reddit](https://www.reddit.com/user/livia2lima). Follow me on [Twitter](https://twitter.com/search?q=%23LinuxUpSkillChallenge%20%40livialimatweets&src=typed_query&f=live) for daily updates.
