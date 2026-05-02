<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTickets installation</h1>
This tutorial outlines the prerequisites and installation of an open-source help desk ticketing system namely osTickets.<br/>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- osTickets

<h2>List of Prerequisites</h2>

- To have a vm or physical computer where you want to install ostickets

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a virtual machine or log into a physical computer where we wanna install ostickets
- Create a windows vm that will serve as our client.
- Join the client vm to the domain

<h2>Installation process</h2>

<h3>Downloading the necessay files</h3>
<p>For installing osTickets, we gotta start by downloading the necessary files to our vm/computer, im personally using a vm so hencefoward i will be saying our vm. For this porpuse we could either go and search for them ourselves or download a zip, even though the option of donwloading the zip may appear faster and easier it has the drawback of potentially causing segurity issues due to the simple fact that we dont know if the files on the zip are the original ones or a modified version. Given our situation i think its best to go ahead and search for the files manually. Nevertheless to make the process easier i have compiled a little table with all the requirments and the original links to everyone of them</p>

|Requierment   |Original download link   |
|---|---|
|osTikcets installation files  |https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0   |
|1   |Generic error; server returned bad status code, CLI validation failed, etc.   |
|2   |Parser error; check input to command line.   |
|3   |Missing ARM resource; used for existence check from `show` commands.   |

<p>After you donwload all the files you should have the following files</p>
<img src="https://i.imgur.com/f5kHs53.png"  height="35%" width="35%"/>


<br>
<p>Once that zip file finishes downloading we have to extract the files within it; After the extraction process is done we should have the next files:</p>
<p><code>the heidi sql setup</code></p>
<p><code>the mysql setup</code></p>
<p><code>a folder containing the osticket files</code></p>
<p><code>a folder containing php</code></p>
<p><code>the php manager for iis installer</code></p>
<p><code>the rewrite amd installer</code></p>
<p><code>vc redist compiler</code></p>


<p>Those are the files that we will be using to intall ostickets, it is really important that we execute them in the correct order.</p>

<h3>Installing iis</h3>
<p>To start installing ostickets first we have to install iis.</p>
<p>Think about a webpage, for a webpage to run there needs to be a server somewhere that hosts it and allows the users to connect to it.</p>
<p>With the help of iis, we can give our vm the capacity to act like a server. Which is something that is essential to ostickets functioning.</p>
<p>To install iis we can either go to <code>turn windows features on or off</code> or to the add roles and features option on the server managmente window, which one you chose depends on your operating system</p>
<p>Once there we can simply click on the iis option</p>
<img src="https://i.imgur.com/XdgT50E.png"  height="35%" width="35%"/>
<p>Nevertheless, we have to make sure we also enable the cgi option within the aplication development toggle</p>
<img src="https://i.imgur.com/D9731Ft.png"  height="35%" width="35%"/>
<p>After the installation process for iis is done we can do little test to ensure everything is alright</p>
<p>That test consist in going to the <code>127.0.0.1</code> address in your browser, when you do that something like this should show up</p>
<img src="https://i.imgur.com/jErzqYk.png"  height="35%" width="35%"/>
<p>the <code>127.0.0.1</code> is the loop back address, and its porpuse its to ping to the vm itself, thus to test whether the server within our vm has been created and its hosting a webpage the best way to go about it is to actually try to connect to that webpage using the aforementioned address through the browser</p>
<p>webpages usually run with code, normally some convination of: html, css, javascript</p>
<p>The webpage the we are now selfhosting is no exception it also runs using code and we can actually see that code if we go to <code>C:\inetpub\wwwroot</code></p>
<img src="https://i.imgur.com/oCKY3Gx.png"  height="35%" width="35%"/>
<p>Importantlly, we can not only observe this code. We can actually modify it to turn our self hosted webpage into a totally different webpage.</p> 
<p>And that is exactly what we will be doing to install ostickets, to install ostickets we need to completly rework our defoult selfhosted webpage into a functioning selfhosted ticketing system/webpage.</p>
<p>And in the following steps i will show how, and the reasoning for every step</p>

<h3>PHP configurartion</h3>
<p>php is a programing language primarly used in webpage development.</p>
<p>php is the language that osticket is programmed in; thus, we are required to install it and to configure our iis server to use it before we can use ostickets.</p>

<p>to install php we firslly have to extract the <code>php zip</code> which contains all the files necesarry for the language to be run</p>
<img src="https://i.imgur.com/HHmJDkN.png"  height="25%" width="25%"/>

<p>then we need to create a folder to place those files</p>
<p>for this we need to go to <code>C:\</code> and create a folder called php</p>
<img src="https://i.imgur.com/LFJlr5r.png"  height="25%" width="25%"/>

<p>and then we have to copy all of our php files to that folder</p>

<p>And with that we will have all the files that php needs ready to go</p>
<br>
<br>
<p>Now how iis works is that our iis server whenever it needs to read php files it will try to look for some executable that i can read to know how to processs those files, right now even though those files exist within our vm our iis server doesnt know where to find them</p>
<p>to solve that we need to register a new php version</p>
<p>but iis doesnt have a native function that allow us to do it, thats why we need to run <code>php manager for iis</code> this is a tool that will create the option to register php versions</p>
<img src="https://i.imgur.com/dGq6emB.png"  height="25%" width="25%"/>

<p>Once thats finished we can go to our iis managment console, and we should see a <code>php manager</code> option</p>
<img src="https://i.imgur.com/82etMyo.png"  height="25%" width="25%"/>
<p>that is the option we just created by running <code>php manager for iis</code></p>

<p>after that whole process we can finally register our new php version by clicking the aforementioned option and just clicking the register a new php version button and then just opening the <code>php-cgi.exe</code> from the php folder we previously created at <code>C:\php</code></p>
<img src="https://i.imgur.com/Rj8P2C3.png"  height="25%" width="25%"/>

<h3>Enable url rewrite</h3>
<p>then we have to run <code>rewrite_amd64_en-US</code> to enable url rewrite</p>
<img src="https://i.imgur.com/Z2F3sie.png"  height="25%" width="25%"/>

<p>url re write allows the user or in this case osticket to configure rules to map any given url to any other url</p>
<p>this is better explained with an example, with url rewrite we can for instance take the url <code>http://localhost/article/342/some-article-title</code> and configure rules within our iis server to turn it into <code>http://localhost/article.aspx?id=342&title=some-article-title</code></p>
<p>we need to enable this on our osticket vm bcos os ticket constantlly converts any x url to y url</p>
<p>for instance ostickets needs to switch from <code>http://127.0.0.1/setup/</code> to <code>http://127.0.0.1/setup/install.php</code></p>
<p>and this is type of url switching is essential to its funtioning, manily due to the fact the php files mentioned before expect certain specific url and if those urls are not provided or are provided in a form that is not expected errors may arise</p>

<h3>Microsoft Visual C++ Redistributable</h3>
<p>when you creeate an aplication in the c progaming language family it is almost imposible that you dont rely on libraries</p>
<p>libraries can be think of as reusable code, like functions or classes that other people created and that you are reusing in your own aplication, using libraries is really common but it has a downside apps that are build using any specific library will then need that library to run even after the code is compiled into a <code>.exe</code> file</p>
<p>osticket is affected by that due to the fact that some components it needs for its correct working really on those libraries</p>
<p>for instance we need to install said libraries to use:</p>
<code>certain php extentions</code>
<code>certain iis modules</code>
<code>image processing functions within ostickets</code>
<p>the specific libraries we need to install are the <code>Visual C++ Runtime libraries</code> and to install them we need to run <code>VC_redist.x86</code></p>

<h3>Deploying the webapp</h3>
<p>Now we have everything requiered for the ostickets webapp to run, but how do we actually run it?</p>
<p>Remember the <code>C:\inetpub\wwwroot</code> folder that i mentioned earlier</p>
<p>Well if we simply switch those files with the files that define ostciket we can convert our defoult webpage into ostickets</p>

<br>
<p>to find the necesarry files we can go to the <code>osticket files zip</code> and extract its contents</p>
<p>once the extraction is finished we can just replace the files on the <code>C:\inetpub\wwwroot</code> folder with the files of the upload folder and our default webpage is now ostickets</p>
<img src="https://i.imgur.com/Rj8P2C3.png"  height="25%" width="25%"/>
