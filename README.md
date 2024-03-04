<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align="center">osTicket Installation Guide</h1>
This guide provides instructions for setting up osTicket, an open-source help desk ticketing system.

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Internet Information Services (IIS)</li>
</ul>

<h2>Operating System</h2>
<ul>
  <li>Windows 10 (21H2)</li>
</ul>

<h2>List of Prerequisites</h2>
<ol>
  <li>Set up an Azure Virtual Machine (VM) environment (Windows 10 with 4 vCPUs recommended).</li>
  <li>Download the <a href="https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">osTicket installation files</a> onto your Azure Virtual Machine.</li>
  <li>Enable Internet Information Services (IIS).</li>
  <li>Install Web Platform Installer.</li>
  <li>Install MySQL and configure a username and password.</li>
    <ul>
      <li>For this tutorial, use the following credentials:</li>
      <ul>
        <li>Username: root</li>
        <li>Password: Password1</li>
      </ul>
    </ul>
  <li>Install C++ Redistributable.</li>
  <li>Configure permissions and install osTicket.</li>
  </li>
</ol>

<h2>Installation Steps</h2>

<h3>Installing and Enabling IIS in Windows with CGI and Common HTTP Features</h3>

<p>
  <ul>
    <li>Access the <b>Control Panel</b> on your VM and navigate to <b>Programs</b>.</li>
    <li>Under <b>Program and Features</b>, select <b>Turn Windows features on or off</b>.</li>
    <li>Find <b>Internet Information Services</b> and check the corresponding box to enable it.</li>
    <li>Expand <b>Internet Information Services</b>, then navigate to <b>World Wide Web Services</b> and expand it further to find <b>Application Development Features</b>. Check the box for <b>CGI</b>.</li>
    <li>Ensure that the boxes under <b>Common HTTP Features</b> in <b>World Wide Web Services</b> are also checked.</li>
      <ul>
        <li><b>Check these boxes in Turn Windows Features on or off:</b></li>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/9c4609d9-f1b1-4ee3-9af7-70776269a0b9" height="50%" width="50%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>To verify the settings, open your browser in the VM and enter <b>127.0.0.1</b>. It should load the page for Internet Information Services.</li>
      <ul>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/0351bd16-843f-4240-9528-34d5b9e6629e" height="50%" width="50%" alt="Disk Sanitization Steps"/></li>
      </ul>
  </ul>
</p>

<br />

<h3>Downloading and Installing osTicket Files</h3>

<p>
  <ul>
    <li>Download <b>PHP Manager</b> (PHPManagerForIIS_V1.5.0.msi) and <b>Rewrite Module</b> (rewrite_amd64_en-US.msi) from the Installation Files.</li>
    <li>Create a folder named <b>PHP</b> in the C drive of your VM.</li>
      <ul>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/b719b64a-743f-4b05-a1c4-63b768f50352" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>Download the zip file <b>PHP 7.3.8</b> (php-7.3.8-nts-Win32-VC15-x86.zip) from the Installation Files and extract its contents into the previously created <b>PHP</b> folder (C:\PHP).</li>
      <ul>
        <li><b>NOTE:</b> If you encounter a warning sign during download, it means Microsoft Defender Smartscreen in your VM is blocking the download. Navigate to your downloads and click on <b>Keep</b>.</li>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/8efda758-4824-4952-8224-361cef2a6144" height="80%" width="80%" alt="Disk Sanitization Steps"/></li>
      </ul>
    <li>Download and install <b>VC_redist.x86.exe</b> from the Installation Files.</li>
    <li>Download and install <b>MySQL 5.5.62</b> (mysql-5.5.62-win32.msi) from the Installation Files.</li>
      <ul>
        <li>After installation, launch the <b>Configuration Wizard</b>.</li>
        <li>Check <b>Install As Window Service</b>, and keep the Service Name as <b>MySQL</b>.</li>
        <li>Check <b>Modify Security Settings</b> and set the password as <b>Password1</b> for this tutorial.</li>
      </ul>
  </ul>
</p>

<br />

<h3>Configuring IIS and PHP</h3>

<p>
  <ul>
    <li>Open <b>Internet Information Services (IIS) Manager</b> as Administrator.</li>
    <ul>
      <li>Ensure that <b>PHP Manager</b> and <b>URL Rewrite</b> are available in IIS Manager, thanks to the PHP Manager and Rewrite Modules files downloaded earlier.</li>
      <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/f82b7cf9-01aa-451f-92c7-c2592e3c804c"/></li>
    </ul>
    <li>In <b>PHP Manager</b>, click on <b>Register new PHP Version</b> and set the directory to the <b>php-cgi</b> file located in the PHP folder on the C drive (C:\PHP).</li>
    <ul>
      <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/871b67f0-4496-48bc-82eb-9a6f941a020b"/></li>
  </ul>
</p>

<br />

<h3>Installing osTicket</h3>

<p>
  <ul>
    <li>Download and install <b>osTicket v1.15.8.zip</b> from the Installation Files</li>
    <li>Extract the <b>upload</b> folder from the zip file and copy it into the directory <b>C:\inetpub\wwwroot</b> in your VM</li>
      <ul>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/cae6cb01-f2ba-41e1-834d-08b3a1cf2b38" height="80%" width="80%" alt="Installation Steps"/></li>
      </ul>
    <li>Rename the copied <b>upload</b> folder to <b>osTicket</b>, then reload IIS Manager</li>
    <li>In IIS Manager, expand the connection <b>Sites</b> then <b>Default Web Site</b> to click and highlight <b>osTicket</b>. Then, navigate to <b>Browse Folder</b> and click on <b>Browser*.80 (http)</b></li>
    <li>The page for osTicket Installer should now pop up, if it does not, check your directories of your files and folders</li>
      <ul>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/ee1eb7ca-6165-476e-8b11-fed0b9cc3420" height="80%" width="80%" alt="Installation Steps"/></li>
      </ul>
    <li>In IIS Manager, go to <b>osTicket</b> and click on <b>PHP Manager</b> and click on <b>Enable or disable extensions</b> and enable the following extensions</li>
      <ul>
        <li>php_imap.dll</li>
        <li>php_intl.dll</li>
        <li>php_opcache.dll</li>
      </ul>
    <li>Refresh osTicket Installer on your browser to see <b>PHP IMAP Extension</b> and <b>Intl Extensions</b> are checked signifying the extensions are installed</li>
    <li>After configurations locate the php file <b>ost-sampleconfig.php</b> inside the directory <b>C:\inetpub\wwwroot\osTicket\include\</b> and rename it to <b>ost-config.php</b> because osTicket Installer needs to interact with this file</li>
    <li>Now go to the <b>Properties</b> of the ost-config file and go to the <b>Advanced</b> settings in <b>Security</b> and <b>Disable Inheritance</b> to remove all inheritance permissions from the file (essentially making a "clean" object)</li>
    <li>Now add a new Permission, then click on <b>Select a principal</b> and for a new object type "everyone" the click on <b>Check Names</b> to set the Group and click OK. Then check all the boxes on Basic Permissions and then click OK. Now everyone using osTicket should have full permission to use it</li>
    <li>Head to osTicket on your browser and click on <b>Continue</b> then set your <b>System Settings</b> and <b>Admin User</b> until you get to <b>Database Settings</b></li>
      <ul>
        <li>For login information, you can set it to a fake email such as "yourname@helper.com", again it is recommended to have a notepad to keep your usernames and passwords on the standby</li>
      </ul>
    <li>From the Installation Files, download and install <b>HeidiSQL</b></li>
      <ul>
        <li>Go through basic setup then launch HeidiSQL and create a New Session using the username "root" and password "Password1"</li>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/00a7340d-0875-4ead-8b0c-2d8c87707efc" height="80%" width="80%" alt="Installation Steps"/></li>
        <li>You should see this once connected</li>
        <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/44a15d23-59e0-452d-b21e-138a773880d1" height="80%" width="80%" alt="Installation Steps"/></li>
        <li>Create a Database and name it <b>osTicket</b></li>
      </ul>
<li>Once connected, return to the osTicket Installer and enter your MySQL database credentials into the respective fields in Database Settings</li>
      <ul>
        <li>MySQL Database: osTicket</li>
        <li>MySQL Username: root</li> 
        <li>MySQL Password: Password1</li>
      </ul>
    <li>Click <b>Install Now</b> to complete the installation process. osTicket should now be fully installed on your VM!</li>
    <ul>
      <li><img src="https://github.com/jadeblas/osticket-prereqs/assets/161860082/e30de5ff-971c-4343-9709-4726063b62a5" height="80%" width="80%" alt="Installation Steps"/></li>
    </ul>
  </ul>
</p>

<br />

<h3>Clean Up</h3>

<p>
  <ul>
    <li>Delete the <b>setup</b> folder inside your osTicket directory located at wwwroot (C:\inetpub\wwwroot\osTicket\setup)</li>
    <li>Set the permissions of <b>ost-config.php</b> to "read only" (only the Read and Read and Execute boxes should be checked)</li>
  </ul>
</p>

