## How to use TailwindCSS with ReactJs

In this article, You will learn how to use [Tailwindcss](https://tailwindcss.com/) in [Reactjs](https://reactjs.org/). This process is not complicated when you do step by step.

_____

**Prerequisites**
- basic understanding in Reactjs
- basic understanding in TailwindCSS

_____

**Step 1:**
         open a terminal or cmd and go to your project folder, then create react app using the following command

```
npx create-react-app myapp 
``` 

Then go to ```myapp``` in the terminal by using the command  ``` cd myapp ``` 

_____ 

**Step 2: **
       Now install the necessary dependencies for TailwindCSS.

```
 npm install -D tailwindcss@npm:@tailwindcss/postcss7-compat postcss-cli autoprefixer@^9
```

Here we use `postcss-cli`, because tailwind requires a CSS build process and step to run the build process we use `postcss-cli`. `autoprefixer` also needs our CSS build process. option ```-D``` means all the dependencies are development dependencies. 

_____

**Step 3: **
Open the project folder `myapp` in your favorite code editor.  I preferred Vs Code.  the open terminal in vs code. Then type the following command to create a full Tailwind configuration file for our project.

```
npx tailwind init --full
```
This command creates the `tailwind.config.js` file.
______

** Step 4:**
Now create a file as `postcss.config.js`. In this file, we going to specify our CSS build process.


> **NOTE:** Both `tailwind.config.js` and `postcss.config.js` must be located in the root of our project folder.

_____

**Step 5:**
Add the following lines in the `postcss.config.js` file.
```
module.exports = {
    plugins: [
        require('tailwindcss'),
        require('autoprefixer')
    ]
};                      
```
______

**Step 6:**
Create a folder as `style` in the src folder. Then create two more files in the `style` folder as follows.

- `tailwind.css`
- `main.css`

______

**Step 7:**
In the `tailwind.css` file add the following files of code. These are basic packages we need to use in our project

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

> `tailwind.css` is an input file and  `main.css` is an output file.

______

**Step 8:**
Open the `package.json` file and add the following scripts below the `eject` script. This script is used to build tailwind CSS.
```
"build:css": "postcss src/styles/tailwind.css -o src/styles/main.css"
``` 
Modify the `start` and `build` scripts as follows.

```
"start": "npm run build:css && react-scripts start"
"build": "npm run build:css && react-scripts build",
```

> sample figure 1
> 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620399221155/_mferMoTU.png)

**Step 9:**
We are in the final step to complete the TailwindCSS with reactjs setup!
Now you can import our `main.css` file into the `App.js` file. `App.js` is enough.  no need to import `main.css` in every component.
```
import './styles/main.css';
```

One last step. Open the terminal in vs code, and type the following command to start build process 

```
npm run build:css
```

now you can add tailwind classes to your components 🥳🥳

Start you react app server and Happy coding! 

```
npm start
```

>sample figure 2
>
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1620400292914/bJREPAclxa.png)


I would love to connect with you at [Twitter](https://twitter.com/verreauxblack) | [LinkedIn](https://www.linkedin.com/in/verreauxblack/).


See you in my next Blog article, Take care!!
________

**Reference : **  
- [Tailwindcss doc](https://tailwindcss.com/docs/guides/create-react-app)
- [React doc](https://reactjs.org/docs/getting-started.html)

_______