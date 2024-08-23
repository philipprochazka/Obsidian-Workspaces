[Work in progress]
**=** Command line options **=** 

Command line options are used to specify various startup options for Mozilla applications. For example, if you have multiple profiles you can use command line configuration options to bypass the Profile Manager and open a specific profile. You can also control how Mozilla applications open, which components open initially, and what the components do when they open. This page describes the commonly used options and how to use them. You can open the command line interface by pressing Shift+F2.

== Syntax rules ==

But first, let's describe the syntax rules that apply for all options.

* Command parameters containing spaces must be enclosed in quotes, such as "Joel User".
* Command actions are case insensitive.
* Command parameters, except profile names, are case insensitive.
* Blank spaces ( ) separate commands and parameters.

== Using command line options ==

Command line options follow the command to start the application. If the option contains arguments, enter the argument after the option. Some options have abbreviations, for example, -editor can be abbreviated as -edit (available abbreviations are described in the text below). In some cases, option arguments must be enclosed in quotation marks (this is noted in the option descriptions below). Multiple command line options can be specified. In general, the syntax is as follows:

  application -option -option "argument" -option argument

=== Examples ===

The following examples show the use of the -ProfileManager command, which will open the profile manager prior to starting Firefox:

==== Windows ====

Select '''Run''' from Windows start menu. Enter the following command:

  firefox -ProfileManager

==== macOS ====

Go to '''Applications ▶︎ Utilities'''. Open terminal and enter the following command:

  cd /Applications/Firefox.app/Contents/MacOS
  ./firefox -ProfileManager

If you use Firefox Nightly, you can enter:

  cd /Applications/FirefoxNightly.app/Contents/MacOS
  ./firefox -ProfileManager

==== Linux ====

Open a terminal and enter the following command:

  cd Firefox installation directory
  ./firefox -ProfileManager

== User profile ==

=== -allow-downgrade ===

Firefox 67's downgrade protection prevents accidentally starting Firefox in a profile running a later version of Firefox. Depending on changes between the two versions, some files in a profile may not be downwards compatible. Adding this option bypasses downgrade protection.

=== -CreateProfile profile_name ===

Create a new profile in the default directory, but do not start the application. The profile will be named <code>profile_name</code> in the profile manager, the <code>profile_name</code> must not contain spaces ( ). Do not run <code>profile_name</code> while running an instance of the application, you can use the <code>-no-remote</code> option to avoid connecting to a running instance.

<pre>firefox -CreateProfile JoelUser</pre>

=== -CreateProfile &quot;profile_name profile_dir&quot; ===

Creates a new profile in the <code>profile_dir</code> directory, but do not start the application. The profile will be named <code>profile_name</code> in the profile manager. Note <code>profile_name</code> and <code>profile_dir</code> are quoted together, and are separated by exactly 1 space (as with the previous syntax, <code>profile_name</code> must not contain spaces).

Do not run <code>profile_dir</code> while running an instance of the application. You can use the <code>-no-remote</code> option to avoid connecting to a running instance.

<pre>firefox -CreateProfile &quot;JoelUser c:\internet\joelusers-moz-profile&quot;</pre>

'''Note:''' <code>profile_dir</code> must not exist and you must not already have a profile called <code>profile_name</code>.

=== -migration ===

Start with import wizard.

=== -new-instance ===

Open new instance, not a new window in running instance, which allows multiple copies of application to be open at a time.

<pre>firefox -new-instance -P &quot;Another Profile&quot;</pre>

'''Note:''' Not available for Windows; see [https://bugzilla.mozilla.org/show_bug.cgi?id=855899 bug 855899].

=== -no-remote ===

Do not accept or send remote commands. Implies <code>-new-instance</code>.

<pre>firefox -no-remote -P &quot;Another Profile&quot;</pre>

'''Note:''' Since Firefox 9, this does really mean what its name implies on all platforms. i.e. instances created with this parameter do not accept or send remote commands, see [https://bugzilla.mozilla.org/show_bug.cgi?id=650078 bug 650078]. That means that such instances won't be re-used. Also when using this argument a new instance is created in any case.

=== -override /path/to/override.ini ===

Load the specified <code>override.ini</code> file to override <code>application.ini</code> (<code>browser/app/application.ini</code>). This can be used to suppress the migration wizard at startup by loading the following <code>override.ini</code>. '''Firefox''' only.

<pre>[XRE] EnableProfileMigrator=0</pre>

=== -ProfileManager ===

Start with profile manager. Short form: <code>-P</code> without a profile name.

=== -P &quot;profile_name&quot; ===

Bypass profile manager and launch application with the profile named <code>profile_name</code>. Useful for dealing with multiple profiles.

<pre>firefox -P &quot;Joel User&quot;</pre>

'''Note:''' <code>profile_name</code> is case sensitive. If you don't specify a profile name then the profile manager is opened instead.
You must use an upper case <code>P</code> on Linux with versions older than 7.x, as there lower case invokes purify mode (memory and leak detection). Other platforms accept both upper and lower case.

=== -profile &quot;profile_path&quot; ===

Start with the profile with the given path. '''Firefox''', '''Thunderbird''' and '''SeaMonkey2.x''' only.

<code>&quot;profile_path&quot;</code> can either be an absolute path (<code>&quot;/path/to/profile&quot;</code>) or a relative path <code>(&quot;path/to/profile&quot;</code>).

'''Note:''' On macOS, specifying a relative path is not supported anymore from Firefox 4.0 and up due to a regression; see [https://bugzilla.mozilla.org/show_bug.cgi?id=673955 bug 673955].

== Browser ==

=== -browser ===

Start with the browser component. '''Firefox''' and '''SeaMonkey''' only.

=== -foreground ===

Make this instance the active application.

=== -wait-for-browser ===

Make the launcher process (Windows only) stay alive until the browser shuts down.

=== -headless ===

Runs Firefox in headless mode, which is very useful for purposes such as debugging and automated testing. Available in Firefox 55+ on Linux, and Firefox 56+ on Windows/Mac OS X.

=== -new-tab URL ===

Open <code>URL</code> in a new tab. '''Firefox''' and '''SeaMonkey2.x''' only.

=== -new-window URL ===

Open <code>URL</code> in a new window. '''Firefox''' and '''SeaMonkey2.x''' only.

=== --kiosk URL ===

Open <code>URL</code> full screen without user interface. '''Firefox 71''' and later.

=== -preferences ===

Open options/preferences window. '''Firefox''' and '''SeaMonkey2.x''' only.

=== -private ===

Opens Firefox in permanent private browsing mode. '''Firefox 3.6''' and later only.

May not be applicable in older Ubuntu for '''Firefox 20''' and later, confirmed to work in 14.04.

=== -private-window ===

Opens a new private browsing window in an existing instance of Firefox. '''Firefox 20''' and later only.

=== -private-window URL ===

Open URL in a new private browsing window. If a private browsing window is already open, a new tab is opened in the existing window. '''Firefox 29''' and later only. Does not work in '''Firefox 31''' on linux mint 17 nor on '''Firefox 48''' on Windows 7. URL opens in a non-private window.

=== -safe-mode ===

If the application is not already running, present the troubleshoot mode dialogue for the default profile. 

Alternatively, present the dialogue for a specified non-running profile. For example: 

<pre>firefox -safe-mode -P JoelUser</pre>

Troubleshoot mode was formerly known as safe mode.

=== -search term ===

Search <code>term</code> with your default search engine. '''Firefox''' and '''SeaMonkey 2.1''' and later only.

=== -setDefaultBrowser ===

Set the application as the default browser. '''Firefox''' only.

=== -url URL ===

Open <code>URL</code> in a new tab or window, depend on the browser option. <code>-url</code> can be omitted. You may list multiple URLs, separated by spaces. '''Firefox''' and '''SeaMonkey''' only.

'''Note:''' When opening multiple URLs, Firefox always opens them as tabs in a new window.

== Other components ==

=== -devtools ===

Start with native [https://developer.mozilla.org/en-US/docs/Tools developer tools] opened.

=== -inspector URL ===

Start with the [https://developer.mozilla.org/en-US/docs/DOM_Inspector DOM Inspector], if installed, and inspect the given URL (where URL is optional).

=== -jsdebugger ===

Start application with [https://developer.mozilla.org/en-US/docs/Tools/Browser_Toolbox browser toolbox]. That is different to Venkman debugger (see option -venkman).

=== -jsconsole ===

Start Firefox with the [https://developer.mozilla.org/en-US/docs/Tools/Browser_Console browser console].

=== -purgecaches ===

Gecko (layout engine) has a JavaScript cache, which is not reset on startup, this clears it.

=== -start-debugger-server PORT ===

Start the debugger server on port. This will enable another instance of Firefox to connect the Firefox developer tools to this Firefox instance. See the article on [https://developer.mozilla.org/en-US/docs/Tools/Remote_Debugging/Debugging_Firefox_Desktop remotely debugging Firefox desktop].

=== -venkman ===

Start with the JavaScript debugger, [https://developer.mozilla.org/en-US/docs/Venkman Venkman], if installed.

The port argument is optional, and if it is omitted, the server will listen on port 6000.

== Linux-specific options ==

Firefox is a GTK app, and as such supports the GTK flags documented [https://docs.gtk.org/gtk3/running.html here].

== Further options ==

Additional arguments may be found with this searchfox search: https://searchfox.org/mozilla-central/search?q=CheckArg%28&path=&case=false&regexp=false
