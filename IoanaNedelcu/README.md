# Ioana Nedelcu

## 25 June 2025
Went through half of the Vue JS exercices, covered basic concepts such as reactivity and the use of `v-if`, `v-bind`, `v-on` and `v-for`.

## 26 June 2025
Finished the Vue JS exercices, delved into more complex topics like lifecycles and child components.

## 27 June 2025
Read through half of Tour of Rust. Found out some new ways to write certain pieces of code (ex. returning values, tuple-like structs) and learned about ownership and borrowing.

## 28 June 2025
Started on the rustlings exercices. Read a couple more chapters of Tour of Rust.

## 29 June 2025
Finished half of the rustlings exercices. These have been helpful in revising the material covered within Tour of Rust. 

## 30 June 2025
Cleaned around the office a little :) And more rustlings.

## 1 July 2025
Finished reading the last chapter of tour of rust. Did rustling exercices on options and error handling, which I found a litlte bit trickier. 

## 2 July 2025
Did rustlings exercices up to unit `18_iterators`. 

## 3 July 2025
Finished rustlings exercices at last. Started on the STM32f4 labs by setting up the board. Ran into an issue where despite our board appearing in the USB listing, the probe couldn't be found. We asked around and this problem turned out to be a pretty common one. In the end we got some help in changing the udev rules and `Config.toml` file, which did the trick.

## 4 July 2025
Looked over the labs proper. We struggled for a while on exercice 9 of `Lab 2 - GPIO`, which involved making a function that takes a letter as an argument and displays it in morse code using 3 LEDs. After much testing we realised the problem stemmed from the fact that we hadn't included a pause between displaying each dot and dash, which explained why no matter which letter we called the function for, all LEDs only lit up once, at the same time. 

## 7 July 2025
Took up my [first issue](https://github.com/WyliodrinEmbeddedIoT/tockloader-rs/issues/45), which involves creating a github workflow CI action that automatically creates  an issue when a folder in the upstream repository is updated. For starters I followed the [Quickstart](https://docs.github.com/en/actions/get-started/quickstart) tutorial on workflows by GitHub to understand the basics of workflow creation. Looking through the examples and use cases in the documentation, I found one on [Scheduling issue creation](https://docs.github.com/en/actions/how-tos/use-cases-and-examples/project-management/scheduling-issue-creation), which might come in handy. Based on this I made a working prototype of the issue creation (based on time alone for now). Tomorrow I will have to modify this workflow to trigger based on repo updates.

## 8 July 2025
The issues are now created based on a trigger. At first I made it so the trigger is on any commit in the repo. After that I managed to make it file path dependent, though I had to change a lot of the code. What's left to do now is to implement this on the actual `tockloader-rs` repository. That being said I still have the problem of my cron job not running at all. Tried a few time intervals but still nothing. I've looked into it and it might just be a huge delay on GitHub's part. I'll have to see if anything changes by tomorrow.

## 9 July 2025
Indeed, the cron scheduling was just a delay on GitHub's part. I checked the log and all of the scheduled workflows ran. Integrated the separate bash script part of the workflow directly into the yml for less file clutter. Had my solution checked and there are quite a few modifications that need to be made. I drafted a flowchart on paper in order to help me figure out the new workflow algorithm (as well as aid in explaining my thought process more easily). It was recommended to me to use the commit hashes in order to figure out which commits were already accounted for, as this was an aspect my intial solution overlooked.

## 10 July 2025
Wrote a list of the steps that I need to take in my implementation. Managed to extract the `sha` of a commit, as well as the one stored in a file. Managed to list all shas up until the one stored in the file.

## 11 July 2025
In the end I've limited my solution to only one workflow, as there were fields I needed in the issue creation that I couldn't pass from one workflow to another. Stored the commit messages as well. Shortened the shas that will be in the issue body. Succesfully created issue listing all of the commits that need updates. Made the check for if issue already exists or not. Editting an issue if it already exists now works. A comment now appears notifying the user if the list was changed.

## 21 July 2025
I forgot to disable the workflows over my vacation but it actually worked in my favor as it turned out to be a great way to debug. I found a few different problems that I need to look over. Firstly, my workflow opened a bunch of new issues, which it isn't supposed to do. It's supposed to only edit an existing one. Second, I realised that as long as the sha in the file is still different, a comment will be left anyway despite the list not having changed at all. These should hopefully be easy fixes as they stem from simple logic flaws in my algorithm that I somehow overlooked.
First problem has been resolved. Turns out all of the issues were created from another workflow I forgot to disable oops. By comparing the old issue body with the newly constructed one comments are now only edited if the list has been changed. I had to make sure the whitespaces for the two matched in order to ensure my comparison works as intended. Added a validity check for stored sha's (checks if the given sha exists in the commits list). This way the workflow won't run infinitely if a faulty sha is provided.

## 22 July 2025
Fixed something that I realised I broke by accident right before I left yesterday. Made it so that the issue is closed when it's up to date and reopened when new updates come in. Ran tests for each situation, as well as checked back on the case of new issue creation and everything seems to work as intended. Tomorrow I will start working on the checker that makes sure shas in the file were updated after a PR (tagged with a specific label).

## 23 July 2025
I finished writing the code for the sha-checker using a timestamp-check based approach but in the end I realised this wouldn't quite work. So instead I'll be checking if the PR contains our sha file within its list of changed files. I had a lot to research but it's gradually taking shape. Managed to extract PR number, list of files changed within it, as well as all of its labels.

## 24 July 2025
Started off by checking if the exclusive label is within the PR's label with simple string pattern matching. Applied the same logic to file checker. Ran negative and positive situation tests for both scenarios. Modified the paths and api links to suit the actual repos and not my dummy ones. The only step left is to create the label and .lastcommsha file in the repository.

## 30 July 2025
Finishing touches on my issue. Struggled a bit with the branching and PR creation but I got some help setting up an SSH key to make the proccess easier. Had to rename my commit to adhere to the `Conventional Commits` check which also proved somewhat tricky.

## 31 July 2025
Started looking into which issue to pick up next. Right now I'm thinking of picking up one which someone else dropped, issue [#41](https://github.com/WyliodrinEmbeddedIoT/tockloader-rs/issues/48). Looked into the `micro:bit` and `tockloader-rs` installation.

## 1 August 2025
Succesfully installed tockloader. Looked over and understood the code that my colleague made for this issue, just have to test it. I've ran into a few issues while trying out the install command, I'll have to ask abt them next time at the office.

## 4 August 2025
Installed `libtock-c` in order to build the example apps. Went in circles a little bit trying to fix an error that I get trying to connect to the micro:bit but I have a new lead that I will try tomorrow.

## 5 August 2025
Turns out I was having debug probe connection problems because the board was connected in maintenance mode. Install seems to work but the app ('blink' from the libtock-c examples) won't run. The installation log is also kind of vague, it just shows 16 pages being written with no completion message. Imported the working 'listen' command that my colleague developed and it's been helpful in troubleshooting. Tried installing a different app as well ('buttons'), same sitution. On 'info' and 'list' commands I get 'App data couldn't be parsed.'. I've been checking with the 'listen' command to observe if the number of bytes allocated to the code section changes after install. It did inbetween 'blink' installs but not after 'buttons' install. I should look over the 'install', 'info' and 'list' code, as well as make sure the '.tab' files aren't corrupted.

## 6 August 2025
Got a side task to do so I took a break from the issue I've been working on. Looked over a colleague's code to ensure all changes from upstream were carried over.

## 7 August 2025
Got 'install' and 'info' commands to work (I wasn't calling them properly). In order to figure out where the problem stems from, I've managed to install an app using python tockloader's 'install' command. I've had problems getting the app to show with 'list' but it seems I was just not booting the 'micro:bit' in the right mode. I've had conflicts between the multiple iterations of tockloader I have installed but I got it figured out now.

## 8 August 2025
App installed with our command shows up on app list but won't start on boot (despite being the only app enabled). Getting 528 error since disabling the working app and I can't seem to put the board into bootloader mode again. As such, I am locked out of 'install', 'uninstall', 'enable' and 'disable' commands. I temporarily fixed the issue that supposedly erased the app region of the board but after changing modes the error is back. Should try 'listen' command to see how the memory allocation has changed.

## 9 August 2025
Tried install without using tockloader tools since I can't get into bootloader (probe?) mode. I tried quickly fixing the install I was given since it doesn't seem to require bootloader mode but this didn't really work out.

## 19 August 2025
Started looking into a side issue ( [#83](https://github.com/WyliodrinEmbeddedIoT/tockloader-rs/issues/83) ) having to do with my first issue. Have to generate the downstream end variable using github actions instead of hardcoding it.

## 20 August 2025
Opened up a new branch for the issue. Made the neccesary adjustments, though I'm not entirely sure if they're enough to satisfy the task. I'm also not sure my test ran, will do another run tomorrow (the edits history for the issue body doesn't show any recent edits). The tasks also only mentions modifying the `issue-builder` workflow but I'm assuming I have to modify the `sha-checker` workflow too, as it also mentions the downstream repository.

## 21 August 2025
Realised workflow dispatch doesn't work from branches so I had to modify my mock repository to test. It seems to work fine, I'll have to ask and see if what I did satisfies the task entirely. Tried fiddling more with the microbit to fix the error I got. I asked around and there's no way around it, I'll have to flash the bootloader and Tock again.

## 22 August 2025
Looked more into the concepts of UPSTREAM and DOWNSTREAM repositories to make sure I fully grasp the task I was given for issue [#83](https://github.com/WyliodrinEmbeddedIoT/tockloader-rs/issues/83) . Also looked a bit into Markdown formatting and code snippet linking for more efficient communication within Github spaces. Did some finishing touches, squashed my commits and opened a pull request.
