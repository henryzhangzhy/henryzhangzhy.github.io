---
author: Henry
topic: Journey
comments: true
---

The complexity of the world increases, while the interface is not properly designed to be easy to use.

Recent time has been taken largely by fixing all kinds of bugs without much progress in my project. I would like to make some notes about them.

1. Install Ubuntu for a work station in Lab.
   - not knowing how to enter BIOS for the motherboard. It seems that different brands try to be very diverse in choose which key as the entry.
   - being blocked by black screen
     - first thought was bootable device is not made properly, but same result with two USBs.
     - after tons of searching, find that there might be an issue with the graphics card TITAN, solution is to disable some settings before install.
     - old solution is to press Ctrl + e to enter settings, I tried but nothing show up and realized that the settings havd been moved to another menu buttom in this version of Ubuntu 16.04.5 install package. Which I guess is designed to make it easier but not consistent with past solutions.
   - successfully installrf Ubuntu. But after installing the latest NVIDIA driver, the computer failed to login.
   - I reinstalled the system again, installed an older version of NVIDIA driver and it worked.

2. DELL AIO computer, monitor brightness adjustment.
    - no buttom found on the monitor
    - mannul says you can adjust the brightness with a control button.
    - nowhere tells where the control button is.
    - sovled using Ubuntu system tools. search for brightness and lock.

3. Duplex printing in Ubuntu.
    - printer is connected using ethernet cable. Printing pdf in chrome works, but no duplex printing in settings. Using system dialog cannot find the printer.
    - why system cannot find the printer while chrome can print? I tried to look for the driver and realized that I had the driver hplip, which satisfied the minimum requirement. But when I tried to run hp-setup, search printer through ethernet, error in python encoding happened.
    - I then upgraded the hplip to the latest version. It can find the printer, but adding the printer would require the password.
    - Jason told me that using only ip address can print on an Android device. I tried and succeed.
    - Why adding a printer that is available through chrome and Android without password would require a password in Ubuntu? And why chrome cannot allow duplex printing for this printer while it can in Android?

4. Autoware compile error.
    - Autoware master branch compiled successfully while a branch we developed failed. It failed because some required message headers for a package is not compiled.
    - Dependency check shown that the header is listed in dependency. Mannually compiling the required messages made the package compile properly.
    - Try to build with a single process ```catkin_make -j1``` succeed.
    - Double checking generated topological order of building packages is correct. But the messages is only a few packages ahead the package that requires it in the order.
    - So the issue actually comes with multi-processing. While ROS figured out the correct order, there is no lock to enforce the order in multi-processing. Thus before the message is finished building, another process started building the package that would require it, which caused the problem.

Human relies heavily on patterns to live on this world. They are good at getting patterns, but are also easily overfitted. While nobody said that monitors must keep a buttom for adjusting brightness, I have already been used to that pattern. We definely need to make changes to the world. Dell might think that without the buttom would make the design simpler and save material. I would agree with that, but as what has been pointed out in [design patterns](https://henryzhangzhy.github.io/2019/08/12/design-patterns-reading-notes.html), we are really far from making it easier for human to learn from experience. Afterall, this is not even pointed out in the mannul. The same pattern can be found in the change of a setting in Ubuntu installation process.

I spend time to note this down, not to waste more time, but to express the concern about such a trend. The trend that increasing complexity of the world will make people suffer. While people with certain level of searching skills like me can try to solve it, would the general audience just give up in terms of such problems? I believe that we should think about the structures, or patterns behind these petterns that would cause great inconvenience in the future world. And try to think about ways to address them properly as early as possible.