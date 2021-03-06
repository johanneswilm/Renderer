
About
=====

This is the Objavi Renderer, which converts HTML files to PDF.
It is a part of the Objavi publishing engine (github.com/sourcefabric/Objavi).

To create the PDF output from HTML pages Objavi Render uses the BookJS
library (github.com/sourcefabric/BookJS) and the WebKit layout engine
(www.webkit.org).

The Objavi Renderer is developed and maintained by Borko Jandras
(borko.jandras@sourcefabric.org).


Copying
=======

Objavi Renderer is free software, distributed under the version 3 of the
GNU Affero General Public License.  The text of the GNU Affero General Public
License is available in the LICENSE.txt file inside the source tree and also
online at http://www.gnu.org/licenses/agpl-3.0.html


Compiling
=========

The BookJS library uses features inside WebKit which are currently available
only in the development version of WebKit, so you'll need to compile WebKit
yourself from source. For this task you also need version 5 of the Qt framework.

Get the sources from WebKit's SVN repository (I recommend that you use
the chromium/1271 branch of WebKit):

    svn checkout https://svn.webkit.org/repository/webkit/branches/chromium/1271 WebKit

This will check out the sources in the WebKit directory inside the working
directory.  From there on follow the build instructions for the Qt port of
WebKit (QtQebKit) which are available on http://trac.webkit.org/wiki/QtWebKit.

For example, if Qt5 is installed in /opt/qt5, the command to build WebKit would
look somewhat like this:

    WEBKITOUTPUTDIR=$PWD/WebKit-build WebKit/Tools/Scripts/build-webkit --qt --qmake=/opt/qt5/bin/qmake --no-video --no-webkit2 --no-webgl --release

To compile the Renderer go to Renderer/src directory and issue the following command:

    QMAKEPATH=WebKit-source/Tools/qmake/ /opt/qt5/bin/qmake WEBKIT_DIR=WebKit-build

substituting WebKit-source with the full path to the WebKit source (where you
checked out the WebKit repository) and WebKit-build with the full path to the
WebKit build directory.


Running
=======

The Renderer can be run in two modes: normal and the GUI mode.

The GUI mode displays a window that looks and behaves just like a normal web
browser would.  This mode is intended for BookJS developers to test how BookJS
behaves inside the WebKit engine.  To do this you can select the
"Install BookJS" button inside the Tools menu.
You can also fire up the standard WebKit developer console and experiment.
To start the Renderer in the GUI mode use the "-gui" command line option.

The normal mode, also called the offline mode, is intended to convert web pages
to PDFs from the command line.  To run the Renderer in this mode specify the
URL of the web page you want to convert to PDF as the command line argument.
Other command line options are:

  * -bookjs -- specifies the location of the BookJS code to use for formatting the page
  * -custom-css -- specifies the CSS text to append after all other CSS text
  * -output -- specified the output file where the PDF should be written to
