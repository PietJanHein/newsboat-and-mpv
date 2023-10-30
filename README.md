# newsboat-and-mpv
config-files for newsboat and mpv

Here files and instructions to set up Newsboat and mpv. 


Newsboat

make a directory ~/.newsboat and untar newsboat.tar.

In the config file you specify the key-functions, the highlighting and some user-preferences. For example, with "highlight all ---.*--- yellow" it will make the titles yellow. Choose whatever color you like: black, red, green, yellow, blue, magenta, cyan, white.
With "bind-key <key> <function>" you specify what keys to use for ordinary functions, it has vim-bimdings and arrows for the normies like it is configured now (I got this from somebody else).
There is a second group of function-keys: for user-specified functions. This you do with "macro <key> <function>. The macro-key is the comma key. I will give one example: "macro b set browser "mpv --ao=pulse" ; open-in-browser ; set browser linkhandler" will open the video in mpv with PulseAudio (to prevent it from using pipewire which is the default on mpv these days, it doesn't work with my soundcard). So wherever you see "macro <key> <function> in the config file then just try it out by hitting the , and then the <key> (comma b for playing a video in mpv). As you can see in the config: press the ? to see all the regular function-keys.
I think that you will be able to figure out the rest yourself, there is a lengthy manpage.

In the urls list you simply put all the feeds. I send mine as an example, if you immediately understand it then skip the rest of this alinea.
For every category you use whatever you defined in the config, in this case " --- <category> ---" and then you get the in the config specified color. (I might remove the " ", I think it looks better that way)
Then you just paste the links to the channel_id's: https://www.youtube.com/feeds/videos.xml?channel_id=<channel_id>, I find those by going to the channelpage, view page source and then ctrl-f on channel_id, after a few jumps you get it. After the link you type the name of the channel, this is just for yourself, the RSS-feeder uses the official channel-name. If you'd like you could also easily use multiple files as urls-file (one for videos, one for articles, whatever) by simply making a script which copies from one file to ~/.newsboat/urls and only after that starts newsboat. 😉

One more advice, if you want to easily sort all the channels then simply use the sort-program on your system (comes with a minimal install): sort -k 2 <inputfile> > <outputfile> , the -k option specifies on which collumn (I would guess that it is being detected based on one or more whitespace) the sorting is done. So first put all the links of one category and the names which you give for the channel or feed (all starting with either a capital letter or small letter, otherwise you get problems with sorting) in a separete file, sort it to another file and then copypaste it into .newsboat/urls , the easiest way to do it if you like to sort it.


mpv

Untar  mpv.tar in ~/.config.mpv/
mpv will look for an input-file, config-file and scripts directory at that path when you start mpv.


mpv.conf

--osd-level=0 disables the OSD when the mouse is above half of the width (in my case the upper 720 pixels) of the monitor. Nice! No OSD in the way while watching a video and accidentally moving the mouse
[big-cache] speaks of itself, why not? You have the hardware for it.
--volume=<value> self-explanatory, default-volume, experiment with it, on my soundcard and headphones (HiFiman, those beat the Sennheiser HD700 big time) 40% is quite loud.
I have some more options in it which I hashtagged out, see what you like, this way you know the options.


input.conf

This just contains all the hotkeys for mpv, it is very simple, when you see a hotkey hashtagged out lower in the file then that is the default hotkey for it, you can override it by removing the hashtag and then defining whatever hotkey you like. You can use more than one hotkey for the same function if you like. I pust those on top because that is easier. I also put some hashtagged default function-hotkeys high in the file just to remember those because I use those, like subtitles. I made the hotkeys a bit more sensible than default, for example f for fullscreen and k, j and h as extra keys to pause and skip time (because we are used to it in the browser).
One hotkey which you might want to know immediately: you can either quit mpv and not have mpv 'remember' where you was and what volume you had and all that by pressing shift+q (Q) or you can have mpv 'remember' all that by pressing q. In the 2nd case mpv simply writes a little file which stores those settings for that video and the next time that you open it that file gets read and it resumes where and how it was.


Scripts

You can easily find a lot of scripts on Github including on the main page for mpv. Most of the time it is as simple as putting those scripts and if required directories in the ~/.config/mpv/scripts directory and then it works after you start a new instance of mpv. Usually the scriptwriter explains how to do it. I will share 2 scripts which I use:

    chapters in mpv (it is in the time-bar and you can hit the tab-key and then select a chapter, you can also change the color of font if you like (the script uses a JavaScript-file)

    playlistmanager, it allows you to start playlist in mpv and select any other video on that playlist via a menu (sort of like an OSD which you only see if you press a hotkey) in mpv. This works both for YT-playlists and for every video in a directory (if you watch a TV-show then simply hit the > or < to go to the next or previous episode if it is sorted on episode-number and you have all the videofiles in the directory itself (no sub-directory).


You could for example also add a sponsorblock-script and much more. mpv is like dwm in that sense, it is meant to be customized, lot of possibilities. Higher threshold for new users but more satisfactory once set up to your liking.
Take into consideration that some of the scripts override the user-specified hotkeys in input-file, the hotkeys specified in the scripts get priority.

