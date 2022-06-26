# Maze Repo

## Description

>You are about to witness a repository that has more than it meets the eye! Some think it as a maze but I would say it's the mirror that deceives you the most :)
nc xx.xxx.xx.xxx xxxxx

## TL;DR

Find .git repo in backup folder, dump and use git extractor to find users.db, crack hash and login.

## Solution

The web page shows a login page.

<img src="media/image1.png" style="width:3.80072in;height:3.85436in" alt="Graphical user interface, application Description automatically generated" />

Initial directory and file scanning revealed a backup folder in the site.

<img src="media/image2.png" style="width:6.26806in;height:2.50625in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

The backup contains a users.db that has nothing inside.

<img src="media/image3.png" style="width:4.95833in;height:2.32292in" alt="Graphical user interface, application Description automatically generated" />

At this point, I relooked at the challenge title description and how it was hinting at git (repository, mirror). Navigating to backup/.git confirms my suspicions.

<img src="media/image4.png" style="width:5.48958in;height:5.57292in" alt="Table Description automatically generated" />

The intended way to discover this was probably to scan for hidden files and directories.

<img src="media/image5.png" style="width:6.26806in;height:2.33958in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

There are tools online to help download the entire .git repository. I used [gitdumper](https://github.com/internetwache/GitTools/tree/master/Dumper) from [GitTools](https://github.com/internetwache/GitTools).

<img src="media/image6.png" style="width:6.26806in;height:6.52083in" alt="Text Description automatically generated" />

Tried to view the commit history using “git log” but there was nothing there.

I used the [extractor](https://github.com/internetwache/GitTools/tree/master/Extractor) script from GitTools to extract commits as the repository seemed to be broken. Three commits were found and it gave me three versions of users.db.

<img src="media/image7.png" style="width:6.26806in;height:1.95903in" alt="Text Description automatically generated" />

Looking through the commit data shows that the database was added and then subsequently removed.

<img src="media/image8.png" style="width:6.26806in;height:1.32569in" alt="Text Description automatically generated" />

<img src="media/image9.png" style="width:6.26806in;height:1.28958in" alt="Text Description automatically generated" />

Looking through the users.db shows us some login credentials.

<img src="media/image10.png" style="width:6.26806in;height:2.60903in" alt="Graphical user interface, application Description automatically generated" />

[Crackstation](https://crackstation.net/) was able to find two of the hashes.

<img src="media/image11.png" style="width:6.26806in;height:3.32986in" alt="Graphical user interface Description automatically generated with medium confidence" />

Logging in as michael:halloween would give us the flag.

<img src="media/image12.png" style="width:6.26806in;height:1.79861in" alt="Graphical user interface, text, application Description automatically generated" />
