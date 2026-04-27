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

- Have a vm or physical computer where you want to install ostickets

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a virtual machine or log into a physical computer where we wanna install ostickets
- Create a windows vm that will serve as our client.
- Join the client vm to the domain

<h2>Installation process</h2>

<h3>Downloading the necessay files</h3>
<p>For installing osTickets, we gotta start by downloading the necessary files to our vm/computer, im personally using a vm so hencefoward i will be saying our vm.</p>
<p>For this porpuse we could either go and search for them ourselves or download the zip files that the kind souls of the internet had create for us, the later is the simplest one so thats what im going to be using.</p>
<a href="https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0">osTikcets installation files</a>
<br>

<br>
<p>Once that zip file finishes downloading we have to extract the files within it; After the extraction process is done we should have the next files:</p>
<p><code>the heidi sql setup</code></p>
<p><code>the mysql setup</code></p>
<p><code>a folder containing the osticket files</code></p>
<p><code>a folder containing php</code></p>
<p><code>the php manager for iis installer</code></p>
<p><code>the rewrite amd installer</code></p>
<p><code>vc redist compiler</code></p>
<img src="https://i.imgur.com/f5kHs53.png"  height="35%" width="35%"/>

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

<p>afterwards we need to run vc_redist</p>
<p>a lot of the code for php extentions and some iis modules was originally writen on c, c++ to be able to actually use those files we need to install vc_redist</p>

<p>after all of that is done we need to restart our iis serve</p>
<p>we do this to avoid certain problems that may araise if some file routes and modules are not actualised</p>

<p>Now rember</p>
