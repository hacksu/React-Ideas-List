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

### A class! A class!

To do anything more complicated we'll going to need to create a class.
Because this isn't ES6 we'll have to do it the old fashioned way and call
`React.createClass`. We'll pass it a dictionary (a list of values
associated with a strings) which for now only one member `render`.
This will get called by React anytime it thinks for some reason our view
needs changed. So

`var IdeaList = React.createClass({
    render: function() {
        return <div>Hello World </div>;
    }
`

In  `ReactDOM.render(` replace everything we have right now with


        ReactDOM.render(
                <IdeaList/>
                document.getElementById('react')
        );

Now when you reload you should see `Hello World` instead of `Hello
HacKSU!``

Lets talk about props for a second. Elements in react can be passed props
by their parents, these could be strings or entire classes and functions.
Inside our render function we can access them inside `this.props.*`
Anytime any of them change the class will be recreated by react and
`render` recalled. Let's add an array of ideas we'll pass to IdeaList

`<IdeaList data={[{title: "1"}, {title: "2"}]}/>`

The brackets (`{}`) tell JSX that the data inside should be put into the
result.

Inside `IdeaList` we need to turn this into a list of element. This might
seem like it would be hard but it's really not.

        React.createClass({
                    "render": function () {
                        var items = this.props.data.map(function(item) {
                            return <li><div>{item.title}</div></li>
                        });
                        return <ul>
                                    {items}
                               </ul>
                    }
                })

### A form

Right now we can't actually change anything. Lets make a form to change
that.


        var IdeaForm = React.createClass({
            getInitialState: function() {
                return {title: ''};
            },

            "submitted": function (e) {
                e.preventDefault();
                this.props.onSubmit(this.state);
                this.setState({title: ""});
                return false;
            },

            titleChange: function(titleField) {
                this.setState({title: titleField.target.value})
            },

            "render": function () {
                return  <form onSubmit={this.submitted}>
                            <input type="text" name="title" value={this.state.title} placeholder="Title" onChange={this.titleChange}/>
                        </form>
            }
        });
There's a lot going on here so lets go over a bit of it. First some of
you may have been scratching heads when you heard that React recreates
classes anytime things change. The solution to this is `state`. State is
retained even if the instance is re-instantiated. Also when it's updated
things are re-rendered. Here we have a form. Any time the form changes
`this.titleChange` is called and from that function `this.setState` is called to
update the state.

Finally when the form is submitted `submitted` is called and the entire state is
passed to a function which is given as a prop to the element.

To use this we just need to use this code:

        function log(state) {
            console.log(state);
        }
        ReactDOM.render(
            <div>
                <IdeaList data={[{title: "test"}, {title: "test"}, {title: "test"}]}/>
                <IdeaForm onSubmit={log}/>
            </div>,
            document.getElementById('react')
        );

Now we have our form and when ever we press enter we'll see the text in the
console.

