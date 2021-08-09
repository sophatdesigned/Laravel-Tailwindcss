
## Step 1: Fresh Laravel Installation
I created a new laravel application on my machine named LaravelTailWind with following command

```sh
laravel new LaravelTailWind
```

This command will create a new Laravel project on my machine with the basic laravel directory structure.
Next Up, We will start with the `TailWindCSS` installation, Import the project in your editor / IDE.

## Step 2: Install TailWind via NPM

We will install TailWind via node package manager
To run the npm command make sure you have node installed on your machine. To check if it is installed go to your terminal / command-line and run comand node -v, If this gives you the version number of node installed on your machine, you are good to go. If not then first you have to install node.

Open Terminal / Command-line and navigate to the project root directory and run the following command.
```sh
npm install tailwindcss
```

This will fetch the required dependencies and will install tailwindcss on your project. You should see a new folder named tailwindcss inside node_modules folder in your project.

## Step 3: Add TailWind to CSS

Now, we are ready to use tailwind css in your project. By default Laravel project comes installed with Bootstrap as a default front-end framework. Since we are going to use tailwind css we will remove the bootstrap imports and replace them with `tailwindcss`.
Open file `app.scss` which is located under folder `resources>sass`.
Remove the following import from the file
```sh
// Fonts

@import url('https://fonts.googleapis.com/css?family=Nunito');
// Variables
@import 'variables';
// Bootstrap
@import '~bootstrap/scss/bootstrap';
```
Replace the content with the following imports
```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

## Step 4: Create your Tailwind config file
Next up, we need to generate a tailwind config file, This fill will be used by laravel mix (webpack) while converting the `scss` file into `css`.
Run the following command to generate the config file.
```sh
npx tailwind init
```
This command will generate tailwind.config.js file in your project root directory.
```
// tailwind.config.js
module.exports = {
theme: {},
variants: {},
plugins: [],
}
```
## Step 5: Include Tailwind in Laravel Mix Build Process

Next up, we need to tell Laravel Mix (which internally uses webpack) to compile tailwind sass using the tailwind configuration file.
Open the `webpack.mix.js` file and make the following changes.

```sh
const mix = require('laravel-mix');
/*
|--------------------------------------------------------------------------
| Mix Asset Management
|--------------------------------------------------------------------------
|
| Mix provides a clean, fluent API for defining some Webpack build steps
| for your Laravel application. By default, we are compiling the Sass
| file for the application as well as bundling up all the JS files.
|
*/
mix.js('resources/js/app.js', 'public/js');
    const tailwindcss = require('tailwindcss')
    mix.sass('resources/sass/app.scss', 'public/css')
    .options({
        processCssUrls: false,
        postCss: [ tailwindcss('tailwind.config.js') ],
})
```
## Step 6: Run NPM

We are now ready to run the npm build process, run the following command in your terminal / command-line
```sh
npm install
```
```sh
npm run dev
```
This will compile you `tailwindcss` code and will put them into app.css file located in `public/css` directory.
That’s all about the installation.

## Step 7: Test


```sh
<link  href="{{ asset('css/app.css') }}"  rel="stylesheet">
```

And I posted this code to test tailwind utility based css framework.

```sh

<div  class="md:flex container border p-4">
    <div  class="md:flex-shrink-0">
        <img  class="rounded-lg md:w-56"  src="https://www.history.com/.image/ar_233:100%2Cc_fill%2Ccs_srgb%2Cg_faces:center%2Cq_auto:good%2Cw_1920/MTU3ODc5MDg3MjM5Mjc1ODQ5/an-aerial-view-of-the-angkor-wat-temple-2.webp"  alt="">
        </div>
        <div  class="mt-4 md:mt-0 md:ml-6">
        <div  class="uppercase tracking-wide text-sm text-indigo-600 font-bold">Angkor Wat</div>
        <a  href="#"  class="block mt-1 text-lg leading-tight font-semibold text-gray-900 hover:underline">
        Where Is Angkor Wat?
        </a>
        
        <p  class="mt-2 text-gray-600">
        Angkor Wat is located roughly five miles north of the modern Cambodian city of Siem Reap, which has a population of more than 200,000 people.
However, when it was built, it served as the capital of the Khmer empire, which ruled the region at the time. The word “Angkor” means “capital city” in the Khmer language, while the word “Wat” means “temple.”
Initially, Angkor Wat was designed as a Hindu temple, as that was the religion of the region’s ruler at the time, Suryavarman II. However, by the end of the 12th century, it was considered a Buddhist site.
Unfortunately, by then, Angkor Wat had been sacked by a rival tribe to the Khmer, who in turn, at the direction of the new emperor, Jayavarman VII, moved their capital to Angkor Thom and their state temple to Bayon, both of which are a few miles to the north of the historic site. As Angkor Wat’s significance within the Buddhist religion of the region increased, so too did the legend surrounding the site. Many Buddhists believe the temple’s construction was ordered by the god Indra, and that the work was accomplished in one night. However, scholars now know it took several decades to build Angkor Wat, from the design phase to completion.
        </p>
    </div>
</div>
```
There you go, Here is what I get as the output on screen.
Have fun working with TailWindCSS on laravel.


document:`sophat`
 