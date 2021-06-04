
*******************Why React learn******************

--> React build on jsx which make it easier to develop application
--> Component based architecture forced you to take complex application and 
    break them up into little contain pieces.
    The small little pieces are way easy to maintain, build, test and debug.
--> react is very fast it render and re-render your application quickly
    keeping up to date with the latest changes in your application data.
--> When you lean react you joining an active community of developer, companies, jobs and open-source project.

***********************Nade.js/yarn****************

--> Node.js - Node is a js on the server
--> npm - node package manage this allow us to install various dependencies
      things like yarn, react etc.
 >>npm install -g yarn ----> it installs globally<<
 >>then, restart the window<<

 ***********************live-server****************

 --> live-server is allowed us to run application quickly.
    npm install -g live-server --> it installs globally.

***********************live-server**************
-->loading two libraries by script tag: -
    (1) react library - react can be used to different context there is 
                        "react-vr" virtual reality, "react native" for native application and
                        we are trying to use react with the browser. 
        >>https://unpkg.com/react@16.0.0/umd/react.develipment.js<<
    (2) react DOM library - this allow render the application to the browser
        >>https://unpkg.com/react-dom@16.0.0/umd/react.develipment.js<<
    
***********************our script file**************

--> our script file load by using the script tag inside index.html
    <script src="/scripts/app.js"></script>

***********************Babel*****************
--> we are going install some babel and it's pre-set which help to write jsx
   >>npm install -g babel-cli@6.24.1
   >>babel --help --- if getting response which means success
---> Babel pre-sets are going to install locally in our project.
        They don't give any access and command 
        instead, we just need their code to live in our project
        so, babel-cli take advance of it and actually use it to transform our jsx into those “createElement.call”
---> before install those pre-sets we have to use "yarn init" - this sets our project to use yarn 
        that allow us specify those local-dependencies.
---> babeljs.io-docs-plugins-official Pre-sets-react
            (2) react -- which allow us to use jsx inside our code
            (3) env -- which allow us to use ES6 features like arrow function, const, react and spread operator.

---> "package.json" is the outline of all the dependencies that our project needs in order to run
---> yarn add babel-preset-react@6.24.1 babel-preset-env@1.5.2
---> We install react and env pre-set dependencies but they have their own 
    dependencies, own package.json, own node module they need all of that.
    react and env dependencies and their sub dependencies they all live in
    node-module.
--> we can delete that folder and re-install it.
--> and also, we have one more thing it happened when we run "yarn init" command
    we have "yarn.lock" file once again that something we are not going to change manually changed

---> create new folder in the root of the folder 
        src->app.js
        where we are going to make indecision application and it contain jsx.
        script->app.js 
        it will be auto-generated file that contain createElement staff/all babel transformation
--> start with code that code we want to compile
--> next we specify the output file that's one in public folder
---> next pre-set we want to use 
   babel src/app.js --out-file=public/scripts/app.js --pre-sets=env, react

---> this is going to watch our src/app.js file changes and automaticly 
     create a new public/scripts/app.js file every time it changes deducted and live that command running 
 babel src/app.js --out-file=public/scripts/app.js --pre-sets=env, react --watch
 

*******************************************webpack*********************************

--> webpack - is allow us to organize our js. So, in the end of the 
    when we run our app throw webpack we get the single js file back
    and that file is calling the bundle

--> bundle - is going to contain everything that our application need to run.
        it is going to contain our dependencies and it is also going to contain our application code.

--> 1st define new property in scripts inside the package.json
    "scripts": {
        "server": "live-server public/"
        "build": "babel src/app.js --out-file=public/scripts/app.js --pre-sets=env, react --watch"
    }

---> now I can run the just using this name
        yarn run server
        yarn run build-babel

---> now we add webpack and also in package.json:-
        yarn add webpack@3.1.0

---> run the webpack:
        yarn run build

----> when we try to run the webpack we get the error because there is no configuration file.
        webpack doesn't know what to do? By default, webpack does nothing
        we have to tell how to work with our application other it is not going to do anything.

--> next webpack configuration file(webpack.config.js) in the root of the our application.

--> webpack.config.js - file is a node script. In order to webpack working
    two critical pieces of information we have to give it
    (1) give entry point - where does our application kick off 
            for us it is app.js inside the src folder
    (2) output the final bundle file - so we are creating the one big js file
        and that contain everything which our application need to run.

--> module.export - inside of it we define all the configuration details our webpack build
            and it is node thing. it is way to exports something

--> webpack grab webpack.confg.js file and access whatever we put inside the module.exports


-->more details: webpack.js.org - documentation - entry and content

-->
    console.log(__dirname); -- it contains the path of current location of our project
    module.exports = {
        entry: './src/app.js’,
        output: {-- it is an object which contain two things:
            path: ''.         -- we have to provide the absolute path to this project on our machine. 
            filename: 'bundle.js' -- it can be anything
        }   
    }

    run the on cmd: node webpack.config.js 
    you will get the correct path
    and the path is: C:\Users\Neeti\Documents\react-course-projects\indecision-app

--> but we want to put the file in the public folder instead of root of the project

--> do that we have to look for path manipulation property

--> go on - node path - documentation - path.join

    const path = required('path');
    console.log (path.join(__dirname, 'public'));
    module.exports = {
        entry: './src/app.js' ,
        output: 
            path: ''.         
            filename: 'bundle.js'  
        }   
    }

    --> re-run: node webpack.config.js

    console.log ();
    module.exports = {
        entry: './src/app.js' ,
        output: 
            path : 'path.join(__dirname, 'public')',        
            filename: 'bundle.js'  
        }   
    }

---> delete the script folder and remove the script tag of react and reactDOM inside index.html
        and 
    add the bundle.s file src
    <script src="/bundle"></script>
    and --watch inside package.json in webpack
    webpack --watch -- it will watch the webpack

*********************************import and export***********************************

Example :- 
    ==> utile.js
        console.log("utitle.js is running");

    - and try to run but it is not going to show on console
    because (1) it is not an entry point for our webpack application.
        (2) it is not importing in any file or in the entry file.

    ==> app.js
        import './utitle.js';
        console.log('app.js is runing');

    - and try to sun - success

    ==> utile.js
        console.log("utitle.js is running");
        console.log(square(4));

    - and try to run - error - just because you that import the file you van access everything 
        every variable/function their own local space

--> import - letting use to grape some value from the file but 
        file has to choose export some value as well 

--> two type of exports : 

    (1) default export
    (2) named exports

--> Named export -
        --> export statement get call with curly brasses 
            where we our named exports 
            but these curly braces is not an object definition

        ==> utile.js
                console.log("utitle.js is running");
                console.log(square(4));
                console.log(add(23 + 2));
                export const multi = (a, b) => a * b;
                export {square, add};

        ==> app.js
        import { square, add, multi } from './utils.js';
            console.log('app.js is running')
            console.log(multi(2, 5));

-->Default export - 

    -->Each file can have only one default export
        and we define like this :

          ==> utile.js
                console.log("utitle.js is running");
                const add = (a, b) => a + b;
                const square = (a) => a*a;
                export const multi = (a, b) => a * b;
                export {square, add as default};
                    or
                export default add;

        ---> but for class we can use :
            export default class Header extends React.Component()

   --> default export should be reference that outside the curly braces
    --> and default export is not necessary to grab by name 
        ==> app.js
        import add, { square, multi } from './utils.js';
                or 
        import add from './utils.js';
            console.log('app.js is running')
            console.log(multi(2, 5), square(2));


**********************************import npm module*******************************
--> npm module - which we didn't write
--> go on - npm validator - yarn add validator@8.0.0 - check what you want to import from validator
    like - import validator from 'Validator';
    console.log(validator.isEmail('test'));
    //output - false
--> now we are going to add react and reactDOM by yarn
        yarn add react@16.0.0 react-dom@16.0.0

-->import React from 'react';
   import ReactDOM from 'react-dom';

****************************************babel with webpack***************************************

--> loader - lets you customise the behaviour of webpack when load given file.

--> install two things:
    (1) babel-core: it is very similar to babel-cli which allow to run babel from command like
                    and babel-core run module allow to run babel from tools like webpack.
                    so, by default it doesn’t have any functionaty we still have to configure to use pre-sets
                    we already pickup out.

    (2) babel-loader:  it is webpack plugin .it is going to allow us
                    to teach webpack how to run babel when webpack sees certain file.

        yarn add babel-core@6.25.0 babel-loader@7.1.1 

--> setup the loader inside the webpack.config.js : 
        more details -> webpack.js.org -> documentation -> module

    module.exports = {
            entry: './src/app.js',
            output: {
            path: path.join(__dirname, 'public'),
            filename: 'bundle.js'
            },
    module: {
        rules: [{
        loader: 'babel-loader',
        test: /\.js$/,
        exclude: /node_modules/
        }]
    }

    ** here we told webpack to run babel
         every time single time its sees one of our js file
          excluding node_modules files

--> the only problem is that babel does nothing by default
    in currently we have not told to use env and react pre-sets

--> over in package.json we told to use pre-set by providing 
pre-sets argument. But cannot do that .

--> to do that we have to setup separate configuration file for babel
    in the root of the project, it's needs to be called
    .babelrc

-->.babelrc - is a js file and it allow to take all of the argument passed into the command line and
    just put them in here 

    {
        "pre-sets" : [
            "env",
            "react"
        ]
    }

    ** here we told whenever this project runs babel go 
     ahead and use these pre-sets
     

***************************************Source Map***************************************

--> If we have big application and we stating getting an error.
 It would be really hard to track down exactly where it coming from.

---> because it shows error in bundle.js file.

--> By using source map, we can change the file and 
track down exactly where it coming from.

--> we are setting the single property in webpack.config.js get that done.

--> more details -  webpack.js.org - documentation - devtool

--> property is 'devtool' which get equal to a string.

--> type of source map :
	*development
	*production

--> for now, we are going to focus on development and we are using 
	cheap-module-eval-source-map

--> Every time you change the webpack.config we have to restart your build
	even if you are using '--watch'.
	* '--watch' - is not watching for changes to 
       the webpack.config.
	* it watches to the changes in the application source.

***********************************Webpack Dev Server********************************

--> 'webpack dev server' it's a development server similar
    to 'live-server' but 'webpack dev server' is have some nice future:
     
     * it speeds up the process between changing the application file 
        and we can see those changes inside the browser.

--> more details - webpack.js.org - documentation - devServer

---> 1st we have install devServer 
        yarn add webpack-dev-server@2.5.1

--> there are quite a few property here we actually need one to set up
    in order to take advantages of the webpack dev server and
    this is devServer.contentBase

--> 'devServer.contentBase' - this let us tell the devServer 
        where can find our public files.
    If we don't configure this devServer is not know 
    where to find public assets

--> this is very similarly how we configure 'live-server' in package.json

    devtool: 'cheap-module-eval-source-map',
    devServer: { -- this is an object 
        contentBase: path.join(__dirname, 'public')
        //here we dine the devServer property
         and the path to the index.html
    }

--> Now we have set the script to run devServer and clean house
        * remove build-babel 
        * remove --watch
        *dev-server' : 'webpack-dev-server'

-->Now we don't have two process running (live-server and webpack) 
    instead, we can just use dev-server

*************************New Babel plugins********************************
--> this is going to add support for the class property syntax.
    that's going to allow us to add property right on to classes
    that supposed to just method

--> more details - babeljs.io - documentation - pre-sets/plugins - Experimental pre-sets (scroll down)

-->TC39 - is the organization which js forward and 
        there are various stages that new feature 
        can be in when it's introduces

-->we are looking for stage -2 pre-sets
    * transform-class-property

--> 1st install transform-class-property
      yarn add babel-plugin-transform-class-properties@6.24.1

-->Next configure the feature in the babelrc
    ,
    'plugins' : [
        "transform-class-property
    ]

--> restart the devServer.

--> let's understand with this pre-sets can do by an example :

    * if want to setup an instance property on every
        of 'OldSyntax' we do that by creating the constructor
        function and setting this.property = value;

    * function with binding 

        class OldSyntax {
            constructor() {
                this.name = 'mike';
                this.getGreeting = this.getGreeting.bind(this); --> add this binding and then call again and success
            }
            getGreting() {
                return `h1, My name is ${this.name}.`;
            }
        }
    //instance
    const oldSyntax = new OldSyntax();
    console.log(oldSyntax);
    console.log(oldSyntax.getGreting());  
                        |
     but we know that it is very easy to break that binding 
     specialy for event handlers.
     I we pull the off it's own variable 
     const getGreeting = oldSyntax.getGreeting; -- we are saving the getGreeting into a variable and we call that variable down below\
     console.log(getGreeting()); -- error becasue we broke the binding
     
     --> we have to fixed that by annoying process.
        adding binding (go above)
----------------------------------------------

    * (1) After install the class transform property
     let's see how we simplify the creating the instance

    * (2) Ability to crate function that are not having their binding mashup 

     class NewSyntax {
         name = 'jen'; --> perfectly valid (no need to define the typ eof the variable let, const, var)
        getGreeting = () => {
            return `Hi, my name is ${this.name}. `;
        }
     }

     const newSyntax = new NewSyntax();
     const newGetGreeting = newSyntax.getGreeting;
     console.log(newGetGreeting); -- success
     console.log(newSyntax);
     
----> we can do this without needing to define
        constructor function.  


---> in our project:- 
        this.state = {
            error: undefined;
        }

    ==> is now:
    state = {
        error: undefined;
    }

--> remove the constructor function and 
    convert and event handler (handleAddoption)
    into arrow function


*******************************Passing Children to Component************************************

--> layout component - what if we want to render header and footer 
          and we want the stuff in the middle to be dynamic
          specify to individual page.

--> TO do that we understand by using an example :-

    const layout = (props) {
        return {
            <div>
                <p>Header</p>
                {props.content}
                <p>Footer</p>
            </div>
        }
    }

    const template = {
        <div>
            <h1>Page title</h1>
            <p>This. is my page</p>
        </div>
    }

    ReactDOM.render(<layout content={template} />,
                        document.getElementById('app')); --> reference that prop (content) inside the layout

--> if i want to pass the data into layout compoent 
    so, how we do that 
    by using props

----------------------------------------------------------

--->Above approach we can take but there is different 
    approach to jsx in to your component.

--> to do that we instead of self-closing syntax
    we actually separate opening and closing newSyntax

--> <layout /> = <layout></layout>

--> the cool thing about doing this we can define the 
    jsx right between the layout tag.

--> much like nested jsx and html we can put the stuff right
    inside the layout

    ReactDOM.render((
        <layout>
            <p>this is inline</p>
        </layout>
    ), document.getElementById('app'));

--> currently we are not using it 
    when we pass something in to a component like this 
    we can access it by children prop

-->'children prop' is built in prop as supposed to prop that manually 
    setup our self.

    const layout = (props) {
        return {
            <div>
                <p>Header</p>
                {props.children}
                <p>Footer</p>
            </div>
        }
    }

*************************************React Modal******************************

--> react modal - it's allowed us to make nice looking dialog box
--> more details - react-modal (GitHub) - usage

--> install it 
        yarn add react-modal@2.2.2

--> create new file OptionModal.js
        
        *next import react-modal in indecision-app and
            render it 
            <OptionModal />

--> 'isOpen' - modal should be open and value if it 'true'
--> 'contentLabel' - it is not going to show in the browser 
                it will show only for user who have accessibility devises

        const OptionModal = (props) =>(
               <Modal
                    isOpen={true}
                    contentLable='selected Option'
                >
                    <h3>Selected Option</h3>
               </Modal>
            )
        }

        export Default OptionModal;

--> we use props whether must open or not.
    that means in IndecisionApp we want to track one more piece of state
    currently IndecisionApp just track total list of options 
    and we want it also track 'selectedOption' and the value is 'undefined'
    when user 1st visits on the app there no reason to show modal right way
    it shows when user click what should i do button.

  state {
      options : [],
      selectedOption : undefined
  }

    <OptionModal selectedOption={this.state.selectedOption} />

--> so instead of true it will be {props.selectedOption}.

--> onRequestClose - when user try to close the modal 
    by using Esc key and by clicking outside the modal

            const OptionModal = (props) =>(
               <Modal
                    isOpen={!!props.selectedOption}
                    contentLable='selected Option',
                    onRequestClose={props.handleClearSelectedOption}
                >
                    <h3>Selected Option</h3>
                    <button onClick="this.handleClearSelectedOption">Okay</button>
               </Modal>
            )
        }

        export Default OptionModal;

--> instead of activated alert we want to set the state in handlePick inside the IndecisionApp.

    this.setState(() => ({
        selectedOption: option
    }))


--> Next, we have to set close button for this we have to define
    ne event handler inside IndecisionApp and pass that down to <OptionModal />

    handleClearSelectedOption = () => {
        this.setState(() => ({
            selectedOption : undefined
        }))
    }

    <OptionModal handleClearSelectedOption={this.handleClearSelectedOption} />

******************************Webpack with scss********************************************

--> create new folder styles inside src
--> create new file name is style.scss in styles folder
--> configure the css file inside webpack.config.js file
--> So far, we only use webpack.config file to work with 
    our js file.
    but we can also use the webpack.config file to work with 
    out style files Whether file is scss or css.

--> to do that we have specify the new rule after the existing 
    one rule.

    , test: /\.css$/,  -- those file must end with css extension

--> now we have to specify the two loader :
    -> css-loader - this.is going to allow webpack to 
            load in css assets. It teaches how to take css and
            converted into js representation of that css 
         * more details - npmjs.com/package/css-loader 

    --> style-loader - it takes that css that's in js 
            and adds into dom by injecting style tag
            that our style showing up to the browser.
         * more details - npmjs.com/package/style-loader

--> yarn add style-loader@0.18.2 css-loader@0.28.4

--> once we installing both of these 
        we have to set that inside the rules.

--> up above we specify the one loader because that is needed 
    to run the babel.
    but for css we need both loaders to sum css file.

--> use - it allow use to specify the array of loader
      test: /\.css$/,
      use: [
        'style-loader',
        'css-loader'
      ]
    
    *whenever webpack encounter a css file it's going to read that file
    and it's ging to dump that it's content into the dom
    in a style tag and end result our style showing up.

--> next load the style file inside app.js
    import './styles/styles.css';

--> restart the devServer

--> next goal is teaching webpack how to compile scss into regular css.
    because browser doesn't understand scss but it understand
    css. 
    and we need that tool to convert scss to css

--> you can learn a lot about scss in  - sass-lang.com - learn sass - variable

--> we need to two loaders 
     * sass-loader - if you encounter a scss file go ahead and compile it 
    
    * node-sass - is compiler itself.

--> yarn add sass-loader@6.0.6 node-sass@5.0.0
                                |
    refer to - https://github.com/sass/node-sass/releases/

--> next step is to change the extension form css to scss everywhere
        file - styles.scss
        import section in app.js - import './styles/styles.scss';

--> next load the new loader on to 'use'
      existing one, test: /\.scss$/,  
                    use: [
                        'style-loader',
                        'css-loader',
                        sass-loader
                    ]
    
    ** behind the scene sass-loader is going to use 
             node-sass to convert the file

--> re-sun the devServer

***************************architecture of style***************************************

--> scss support the import syntax by default
    so, we are going to create separate file 
    for import syntax and reuse them in style files

--> create new folder called base 
    which going to container basic style
    like global family font.

--> create new file called '_base.scss' inside the base folder 

--> _base.scss - when we creating the separate file 
                which going to loaded in though
                it's known as partial file and it start 
                with underscore (_).
                this file is containing part of our application style

        baby {
            font-family : arial
        }

  ==> style.scss
            @import './base/base';

---> 'rem' value - is a relative value 
               and rems take their sizing 
                from the root element (<html>).
    more-details - go on mdn else on bootcamp course

--> next we have to work on header:
    * create new folder called 'components' 
            inside the styles folder

    * inside it create new file called _header.scss

    * import in styles.scss file

--> BEM - block element modifier
        B - is a building block something big like header
        E - element that thing which goes inside
                 of the block to make them useful
        M -  modifier 
   .header__title {
       //name is just naming conversion to figure out
       what's going on in this className
   }

   * here we targeting title which is inside the header.

--> Now we are going to install css reset for our styles
 
--> css reset - it makes sure that all browser is 
                started form same place.
                Each browser has their own default styles
                and they not start form same place and they
                look deferent when we apply our style.

--> tool called normalize css
    
--> ad this - yarn add normalize.css@7.0.0

--> next step is to import it in app.js right above.
    and grape the path from normalize directory

    import 'normalize.css/normalize.css';

--> if run this it will crash because 
    we change the ability to support regular css files 
    over inside the webpack.config
    we change fixed the by using question mark (?)

      test: /\.s?css$/, -->now can also loop to css and scss file
      use: [
        'style-loader',
        'css-loader',
        'sass-loader'
      ]

--> so far, some styles value is repeating 
    it is mush easy to put those value one place. so 
    we can change the value at one place and that apply everywhere .

--> now we are going to create common setting file 
    inside the base folder called _seetings.scss
    and import in style.scsss on the top. so the other file 
    can take the advantages of common settings and always
    setting comes first

-->sudo-class
    *.big-button:disabled {
        //it going to apply the button when 
        button is disabled.
    }

--> change cursor
    button {
        cursor: pointer
    }
    button:disabled {
        cursor: default;
    }

--> there is other button that make up the application
    the big-button is pretty special it has lot of
    style attribute:

    . big-button {
            background: $purple;
            border: none;
            border-bottom: .6rem solid darken ($purple, 10%);
            color: white;
            font-weight: bold;
            font-size: $l-size;
            margin-bottom: $m-size;
            padding: 2.4rem;
            width: 100%;
        }

--> those attribute will not share by other button 
    and we don't have re-write the code.
    instread we create new className -

    . button {
        //some style attribute to make small button
    }

--> now we going to create modifier (from BEM) form the small button 
    which going to allow us to do some changes - 

    * so, for button element we do like this:
        . button__dropdown {
            //dropdown is inside button
        }

    * for modifier we two hyphens (--) then we give the name
     to the modifier version of the button:

     .button--link {
        //we called link 
        because it’s going look like link based button
     }

--> inside of className ‘. button--link'
    we can define the changes we want to do 
    compare the original one.

     .button--link {
        //styles value
     }

--> define the className inside the Options.js :

    <button className="button button--link">

--> _widget.scss - it is box and it have header and body down
                    and it going to style box where all 
                        the option appears

--> flex-box - it creates mush nice way to create layout

--> darken () - it just like js function and it take two argument 
                1st color and 2nd is the percentage we want to darken


************************Styling React-modal********************************

--> react-modal is a box and it's not generated by us.
    So how you are going to style it?

--> by using the structure (inside the element panel) react-model already has a place

--> create the new file called _modal.scss 
        inside the styles/component:

-->transition style - it set the element motion.

-->closeTImeoutMS - is prop of react modal and it take the
                    amount of time you want to wait before 
                    getting out from DOM.

-->className - is a custom prop and it means that react-modal
                is going to use the custom style.

--> 1rem = 16px

-->Media queries:-

    *@media (min-width: 45rem) {
        //the style will show on the large screen
        which are greater than 45rem.
    }

     *@media (max-width: 45rem) {
        //the style will show on the small devises
        which are less then 45rem.
    }
    
--> Favicon - is the little icon which shows up
                to the browser tab

--> create new folder called images inside the public folder

--> put image inside of this folder 

--> specify the favicon:
    
    ==>index.html 
    <link rel = 'icon' type='image/png' href='/images/favicon.png'>

--> manually refresh the application in the browser.

/////////////////////////////The End/////////////////////////////////////////////////






