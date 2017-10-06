# Cocoa Custom About Window

Demonstrates how to customize the standard "About <app name>..." window for Cocoa applications.

<img src="./Img/Capture@2x.png" width="585" height="483" alt="Screenshot of the demo project" />

### Background

In the code generated by all Xcode templates, when you select "About <app name>..." in an app's main menu, 
the method:

    - (void)orderFrontStandardAboutPanelWithOptions:(NSDictionary<NSString *, id> *)optionsDictionary

is called on the shared application object, which in turn presents a small window with standard
labels and an icon displaying info about your app, which is exctracted from certain keys in the 
property list (version, copyright, etc.).

However, it would be very difficult to obtain a reference to this window and customize it at runtime. 
The best you are allowed to do is drop a custom `Credits.rtf` file in your resources folder and have
the default _About..._ window pick that up at runtime.

### Features

This project demonstrates how to use a custom window controller and present that instead.
It reads from `Info.plist` all the same keys that the default _About..._ window shows.
But in contrast with the default window, you can fully customize its appearance (because you 
have access to the window controller's source code); e.g. add extra labels, etc. 
In this demo, I have changed the appearance of the window to "Vibrant Dark", much 
like e.g., the [Pixelmator](http://www.pixelmator.com) app.

### How to use it in your projects

1. Copy the following files into your project:

    - AboutWindowController.h
    - AboutWindowController.m
    - AboutWindow.xib

    (If you wish to further customize the information displayed in the About 
    window, Add extra subviews to the xib and define the corresponding outlets 
    in the window controller class. You will need to configure those views with
    whatever information you wish to display, inside the method `-windowDidLoad`)

2. Go to your project's AppDelegate implementation file and add this line near the top:

        #import "AboutWindowController.h"

3. Still in the AppDelegate implementation file, add the following method:

        - (IBAction) about:(id)sender {
        // Show the window:
        [[AboutWindowController defaultController].window orderFront:self];
        }

4. Go to the xib file that contains your app's main menu (by default named "MainMenu.xib")

5. Select the "About..." menu item.

6. In the Connections Inspector (section: "Sent Actions"), remove the action that 
is set by default (`orderFrontStandardAboutPanelWithOptions:`).

7. Control-drag from the (now empty) action slot all the way to the xib file's 
"First Responder" placeholder, and in the list that pops up, choose the action 
named `about:` (this is the method that you defined in step 3).

8. Build and run.

    









