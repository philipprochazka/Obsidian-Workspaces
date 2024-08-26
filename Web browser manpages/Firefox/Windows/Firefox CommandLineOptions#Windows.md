<h1> Firefox Command line options </h1> 

Command line options are used to specify various startup options for Mozilla applications. For example, if you have multiple profiles you can use command line configuration options to bypass the Profile Manager and open a specific profile. You can also control how Mozilla applications open, which components open initially, and what the components do when they open. This page describes the commonly used options and how to use them. You can open the command line interface by pressing Shift+F2.

<h2> Syntax rules </h2>

But first, let's describe the syntax rules that apply for all options.

* Command parameters containing spaces must be enclosed in quotes, such as "Joel User".
* Command actions are case insensitive.
* Command parameters, except profile names, are case insensitive.
* Blank spaces ( ) separate commands and parameters.

<h2> Using command line options </h2>

Command line options follow the command to start the application. If the option contains arguments, enter the argument after the option. Some options have abbreviations, for example, -editor can be abbreviated as -edit (available abbreviations are described in the text below). In some cases, option arguments must be enclosed in quotation marks (this is noted in the option descriptions below). Multiple command line options can be specified. In general, the syntax is as follows:

  application -option -option "argument" -option argument

<h3> Examples </h3>

The following examples show the use of the -ProfileManager command, which will open the profile manager prior to starting Firefox:

<h4> Windows </h4>

Select '''Run''' from Windows start menu. Enter the following command:

  firefox -ProfileManager

<h4> macOS </h4>

Go to '''Applications ▶︎ Utilities'''. Open terminal and enter the following command:

  cd /Applications/Firefox.app/Contents/MacOS
  ./firefox -ProfileManager

If you use Firefox Nightly, you can enter:

  cd /Applications/FirefoxNightly.app/Contents/MacOS
  ./firefox -ProfileManager

<h4> Linux </h4>

Open a terminal and enter the following command:

  cd Firefox installation directory
  ./firefox -ProfileManager

<h2> User profile </h2>

<h3> -allow-downgrade </h3>

Firefox 67's downgrade protection prevents accidentally starting Firefox in a profile running a later version of Firefox. Depending on changes between the two versions, some files in a profile may not be downwards compatible. Adding this option bypasses downgrade protection.

<h3> -CreateProfile profile_name </h3>

Create a new profile in the default directory, but do not start the application. The profile will be named <code>profile_name</code> in the profile manager, the <code>profile_name</code> must not contain spaces ( ). Do not run <code>profile_name</code> while running an instance of the application, you can use the <code>-no-remote</code> option to avoid connecting to a running instance.

<pre>firefox -CreateProfile JoelUser</pre>

<h3> -CreateProfile &quot;profile_name profile_dir&quot; </h3>

Creates a new profile in the <code>profile_dir</code> directory, but do not start the application. The profile will be named <code>profile_name</code> in the profile manager. Note <code>profile_name</code> and <code>profile_dir</code> are quoted together, and are separated by exactly 1 space (as with the previous syntax, <code>profile_name</code> must not contain spaces).

Do not run <code>profile_dir</code> while running an instance of the application. You can use the <code>-no-remote</code> option to avoid connecting to a running instance.

<pre>firefox -CreateProfile &quot;JoelUser c:\internet\joelusers-moz-profile&quot;</pre>

'''Note:''' <code>profile_dir</code> must not exist and you must not already have a profile called <code>profile_name</code>.

<h3> -migration </h3>

Start with import wizard.

<h3> -new-instance </h3>

Open new instance, not a new window in running instance, which allows multiple copies of application to be open at a time.

<pre>firefox -new-instance -P &quot;Another Profile&quot;</pre>

'''Note:''' Not available for Windows; see [https://bugzilla.mozilla.org/show_bug.cgi?id=855899 bug 855899].

<h3> -no-remote </h3>

Do not accept or send remote commands. Implies <code>-new-instance</code>.

<pre>firefox -no-remote -P &quot;Another Profile&quot;</pre>

'''Note:''' Since Firefox 9, this does really mean what its name implies on all platforms. i.e. instances created with this parameter do not accept or send remote commands, see [https://bugzilla.mozilla.org/show_bug.cgi?id=650078 bug 650078]. That means that such instances won't be re-used. Also when using this argument a new instance is created in any case.

<h3> -override /path/to/override.ini </h3>

Load the specified <code>override.ini</code> file to override <code>application.ini</code> (<code>browser/app/application.ini</code>). This can be used to suppress the migration wizard at startup by loading the following <code>override.ini</code>. '''Firefox''' only.

<pre>[XRE] EnableProfileMigrator=0</pre>

<h3> -ProfileManager </h3>

Start with profile manager. Short form: <code>-P</code> without a profile name.

<h3> -P &quot;profile_name&quot; </h3>

Bypass profile manager and launch application with the profile named <code>profile_name</code>. Useful for dealing with multiple profiles.

<pre>firefox -P &quot;Joel User&quot;</pre>

'''Note:''' <code>profile_name</code> is case sensitive. If you don't specify a profile name then the profile manager is opened instead.
You must use an upper case <code>P</code> on Linux with versions older than 7.x, as there lower case invokes purify mode (memory and leak detection). Other platforms accept both upper and lower case.

<h3> -profile &quot;profile_path&quot; </h3>

Start with the profile with the given path. '''Firefox''', '''Thunderbird''' and '''SeaMonkey2.x''' only.

<code>&quot;profile_path&quot;</code> can either be an absolute path (<code>&quot;/path/to/profile&quot;</code>) or a relative path <code>(&quot;path/to/profile&quot;</code>).

'''Note:''' On macOS, specifying a relative path is not supported anymore from Firefox 4.0 and up due to a regression; see [https://bugzilla.mozilla.org/show_bug.cgi?id=673955 bug 673955].

<h2> Browser </h2>

<h3> -browser </h3>

Start with the browser component. '''Firefox''' and '''SeaMonkey''' only.

<h3> -foreground </h3>

Make this instance the active application.

<h3> -wait-for-browser </h3>

Make the launcher process (Windows only) stay alive until the browser shuts down.

<h3> -headless </h3>

Runs Firefox in headless mode, which is very useful for purposes such as debugging and automated testing. Available in Firefox 55+ on Linux, and Firefox 56+ on Windows/Mac OS X.

<h3> -new-tab URL </h3>

Open <code>URL</code> in a new tab. '''Firefox''' and '''SeaMonkey2.x''' only.

<h3> -new-window URL </h3>

Open <code>URL</code> in a new window. '''Firefox''' and '''SeaMonkey2.x''' only.

<h3> --kiosk URL </h3>

Open <code>URL</code> full screen without user interface. '''Firefox 71''' and later.

<h3> -preferences </h3>

Open options/preferences window. '''Firefox''' and '''SeaMonkey2.x''' only.

<h3> -private </h3>

Opens Firefox in permanent private browsing mode. '''Firefox 3.6''' and later only.

May not be applicable in older Ubuntu for '''Firefox 20''' and later, confirmed to work in 14.04.

<h3> -private-window </h3>

Opens a new private browsing window in an existing instance of Firefox. '''Firefox 20''' and later only.

<h3> -private-window URL </h3>

Open URL in a new private browsing window. If a private browsing window is already open, a new tab is opened in the existing window. '''Firefox 29''' and later only. Does not work in '''Firefox 31''' on linux mint 17 nor on '''Firefox 48''' on Windows 7. URL opens in a non-private window.

<h3> -safe-mode </h3>

If the application is not already running, present the troubleshoot mode dialogue for the default profile. 

Alternatively, present the dialogue for a specified non-running profile. For example: 

<pre>firefox -safe-mode -P JoelUser</pre>

Troubleshoot mode was formerly known as safe mode.

<h3> -search term </h3>

Search <code>term</code> with your default search engine. '''Firefox''' and '''SeaMonkey 2.1''' and later only.

<h3> -setDefaultBrowser </h3>

Set the application as the default browser. '''Firefox''' only.

<h3> -url URL </h3>

Open <code>URL</code> in a new tab or window, depend on the browser option. <code>-url</code> can be omitted. You may list multiple URLs, separated by spaces. '''Firefox''' and '''SeaMonkey''' only.

'''Note:''' When opening multiple URLs, Firefox always opens them as tabs in a new window.

<h2> Other components </h2>

<h3> -devtools </h3>

Start with native [https://developer.mozilla.org/en-US/docs/Tools developer tools] opened.

<h3> -inspector URL </h3>

Start with the [https://developer.mozilla.org/en-US/docs/DOM_Inspector DOM Inspector], if installed, and inspect the given URL (where URL is optional).

<h3> -jsdebugger </h3>

Start application with [https://developer.mozilla.org/en-US/docs/Tools/Browser_Toolbox browser toolbox]. That is different to Venkman debugger (see option -venkman).

<h3> -jsconsole </h3>

Start Firefox with the [https://developer.mozilla.org/en-US/docs/Tools/Browser_Console browser console].

<h3> -purgecaches </h3>

Gecko (layout engine) has a JavaScript cache, which is not reset on startup, this clears it.

<h3> -start-debugger-server PORT </h3>

Start the debugger server on port. This will enable another instance of Firefox to connect the Firefox developer tools to this Firefox instance. See the article on [https://developer.mozilla.org/en-US/docs/Tools/Remote_Debugging/Debugging_Firefox_Desktop remotely debugging Firefox desktop].

<h3> -venkman </h3>

Start with the JavaScript debugger, [https://developer.mozilla.org/en-US/docs/Venkman Venkman], if installed.

The port argument is optional, and if it is omitted, the server will listen on port 6000.

<h2> Linux-specific options </h2>

Firefox is a GTK app, and as such supports the GTK flags documented [https://docs.gtk.org/gtk3/running.html here].

<h2> Further options </h2>

Additional arguments may be found with this searchfox search: https://searchfox.org/mozilla-central/search?q=CheckArg%28&path=&case=false&regexp=false
