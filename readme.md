# React Idea Lister

Hi folks. This will be the first of our normal lectures for the semester so I'll
try to keep things simple. This project should have no dependencies to download,
though everything will be easier if you have NodeJS installed and for a lot of
future talks it will make things easier.

Because this is the first talk I want to make clear what my goals here are. If
you disagree please bring it up during a meeting and we can come to a
compromise.

For this more advanced side I think we need to give up on thinking we'll going
to be able to totally learn anything during a meeting. Instead I want people to
know what's out there. So for example if you decided you want to make a website
you'll know ReactJS exists and have some idea of what it's good for.

I'll assume everyone trying to follow my talks is at least passingly familiar
with JavaScript and HTML. If you aren't I'd suggest paying attention to Ben's
talk instead.

## Set Up

Download the starter project from https://github.com/hacksu/React-Ideas-List.
If you have git installed you can clone the repository, if not just download and
extract the zip file. If you don't have a computer that's capable of editing an
HTML file for whatever reason you can also follow along at
https://jsfiddle.net/fysh9bhn/3/

For most people you should just be able to double click `index.html` to load it
into your browser of choice. If that doesn't work for some reason I'll try to
give you a hand. If you want to put scripts in a separate file you may need to
host the files via an HTTP server. Some browser won't load the files from disk.
For that if you have NodeJS installed you can just run
`npm install http-server -g` and then after navigating to the folder you
downloaded the starter project into run `http-server`. Just navigate to  `http://127.0.0.1:8080/` in your browser of choice.