Vim Hurts

To start the challenge, we will need to connect to \`nc 18.141.84.203 61003\` create an instance of the challenge for us. For our instance it was created at http://18.141.84.203:62546/

<img src="media/image1.png" style="width:6.26806in;height:2.06528in" alt="Text Description automatically generated" />

Visiting the web page shows a file upload page. Based on the challenge description, there is a vulnerability in uploading the file. Files uploaded successfully can be found in /uploads on the web server. The folders that were able to be listed can be seen in a figure later on.

<img src="media/image2.png" style="width:2.54647in;height:2.18808in" alt="Graphical user interface, application Description automatically generated" />

Attempts to upload a non-image fails as jpg and png files are allowed only. Techniques such as using different extensions, changing the content type, and even embedding an image with php shellcode still failed.

<img src="media/image3.png" style="width:2.4479in;height:2.40496in" alt="Graphical user interface, text, application Description automatically generated" />

Inside the html source code, the file is being uploaded to the same page

<img src="media/image4.png" style="width:6.26806in;height:1.5625in" alt="Graphical user interface, text Description automatically generated" />

<img src="media/image5.png" style="width:6.26806in;height:2.42917in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

Given the challenge name and the fact that the admin did not exit vim, suggests that a .swp file exists on the server. The purpose of the swap file is to store the recovery version of a file being edited in the program. SWP files also serve as lock files, so no other Vi editing session can concurrently write to the currently open file.

<img src="media/image6.png" style="width:6.26806in;height:1.90625in" alt="Text Description automatically generated" />

We can do a \`vim index.php.swp\` to recover the file open in vim.

<img src="media/image7.png" style="width:6.26806in;height:3.45972in" alt="Text Description automatically generated" />

We go ahead and recover the *index.php* file that was found within the swap file.

![](media/image8.emf)

Upon opening the file in a text editor, it can be seen that several checks are required to pass for the file to be in the /upload directory.

<img src="media/image9.png" style="width:6.26806in;height:4.48264in" alt="Text Description automatically generated" />

In addition, only alphanumeric and “.\_-” characters were allowed in the file name.

<img src="media/image10.png" style="width:6.25087in;height:0.65634in" />

Interestingly, the file is moved to \`/uploads/\` directory before the file is being checked. Files that do not pass the *check_file* function will be sent to be quarantined in /tmp.

<img src="media/image11.png" style="width:6.26806in;height:2.04097in" alt="Text Description automatically generated" />

Since the files will exist in “/uploads/”, we can attempt to serve our web shell before it is quarantined by the server. In addition to that, we can make it such that our web shell will be able to replicate itself as the server will only quarantine the original file.

Our shell script is as follows:

<img src="media/image12.png" style="width:5.7508in;height:0.50007in" />

In addition, we will have another script to continuously curl the webserver to run our *shell.php* on the server.

<img src="media/image13.png" style="width:5.90707in;height:1.7815in" alt="Text Description automatically generated" />

<img src="media/image14.png" style="width:5.90795in;height:0.87971in" alt="Text Description automatically generated" />

Testing our copied web shell at /uploads/webshell.php confirms that it works!!

<img src="media/image15.png" style="width:6.26806in;height:0.55in" />

The flag is found in \`/flag.txt\`

<img src="media/image16.png" style="width:6.26806in;height:0.43125in" />

STANDCON22{v!m_swp_f!l3s_c4n_s3rv3_4tt3ck3rs}
