Injection for Xcode Source
==========================

Copyright (c) John Holdsworth 2012

The source code is provided on the understanding it will not be redistributed in whole
or part for payment and can only be redistributed with the licensing code left in.
License is hereby granted to evaluate this software for two weeks after which if you are 
finding it useful I would prefer that you made a payment of $10 (or $25 dollars in a 
commercial environment) as suggested by the licensing code included in the software
in order to continue using it.

To use injection open the InjectionPlugin project, build it and restart Xcode.
Open a simple example project such as UICatalogue or GLEssentials from Apple
and use the "Product/<ProjectName>Patch Project for Injection" menu item to 
prepare the project and rebuild it. When you run the project it should connect
to Xcode which will display a red badge showing the application is prepared
to load patch bundles. Select an implementation source file and use menu item
"Product/Inject Source" to inject any changes you may have made into the app.

The three projects in the source tree are related as follows:

ObjCpp: A type of Foundation++ set of C++ classes prviding operatiors on foundation objects/

Injection: The original application which worked alongside Xcode as submitted to Apple

InjectionPlugin: The Xcode plugin source packaging the application for use inside Xcode

InjectionInstallerIII: an installer application for the Xcode plugin.

If you find (m)any issues in the code get in contact using the email injection@johnholdsworth.com

Source Files/Roles:

InjectionPlugin/Classes/InInjectionPlugin.m
Singleton subclass of original InAppDelegate class responding to Xcode Menu events.
Also responsible for running up TCP server process on port 31442 receiving connections
from applications with their main.m patched for injection. When an incoming connection
arrives is opens an instance of InPluginDocument associated with the project of the 
application.

InjectionPlugin/Classes/InPluginDocument.m
An instance is created of this INDocument(NSDocument) subclass for each project being
injected. Runs a series of Perl scripts in response to menu events to patch projects
or code for injection.

Injection/Injection/InAppDelegate.m
The original standalone application delegate running the injection service and managing
licensing.

Injection/Injection/InDirectory.m
A utility class for OS X 10.6 where FS events can not be selected down to the file level.

Injection/Injection/InDocument.m
The subclass responsible for running the scripts used by injection to patch projects 
and classes.

Injection/Injection/InImageView.m
NSImageView subclass that knows the path of the file dragged onto it.

Injection/Injection/validatereceipt.m
copy protection formerly used for App Store

Perl scripts:

Injection/Injection/listDevice.pl
Lists the files in the sandbox on an iOS device.

Injection/Injection/openBundle.pl
Opens the bundle project containing the class categories used for injection.

Injection/Injection/openProject.pl
Run when a project is first used for injection to patch main.m and the ".pch" file

Injection/Injection/openURL.pl
Opens special URLs used by injection to patch/un-patch specific files.

Injection/Injection/prepareBundle.pl
The script called when you inject a source file

Injection/Injection/revertProject.pl
Un-patches main.m and the project's .pch file when you are finished injection

Injection/Injection/common.pm
Code shared across the above scripts including the code that patches classes into categories.

Please note:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

