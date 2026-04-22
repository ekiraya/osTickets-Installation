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

<p>For installing osTickets, we gotta start by downloading the necessary files to our vm/computer.</p>
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
