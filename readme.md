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
downloaded the starter project into run `http-server`. Just navigate to  
`http://127.0.0.1:8080/` in your browser of choice.

## Motivation

How many of you have done anything with JavaScript before? What about JQuery?
The problem with trying to build big complicated projects in vanilla JS or React
is that things can get really complicated fast. There's no structure. Trying to
make a single page web app like for example facebook.com get's complicated fast.
Facebook it turns out ran into this too. React is their answer to this problem.

Basically it breaks up your page into reusable elements while making it
really easy to associate code and data with it. Lets make a small example.

## Project

### Hello React

Right now if you load the page you won't see anything. This is just an empty
project right now. The first thing we'll want to do is add some code to tell react to render inside a particular component. Replace where I have
`// we'll wrote our code here` with

        ReactDOM.render(
            <div>Hello HacKSU!</div>,
            document.getElementById('react')
        );

This should simultaneously make sense to those of you who have done stuff
with vanilla JS and confuse you. The part that's standard is that we'll calling a function `render` which is part of `ReactDOM`. You may have even
noticed that we'll selecting the div element `react` by it's id. The
confusing bit is the first argument. It doesn't look like valid
JavaScript. You'd be right. It isn't JavaScript instead it's a small
derivative called JSX that compiles into JavaScript. In the compiled
version it looks a lot ugglier, but what the JSX compiler does is turn
basically standard HTML into all sorts of function calls to build up
React's version of your page. Some may also have noticed that
`type="text/babel"`. This is because there is actually a mini JavaScript compiler called Bable working in the background to convert our script into JavaScript. This is a really bad way to do this in production, but it will
fine for this. In the future we'll assume you've got at least NodeJS and a
text editor installed.

Anyway. If you load this in your browser you should see `Hello HacKSU!`

