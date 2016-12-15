# Setup React project form Scratch

## Create project folder

```
$ mkdir form-scratch && cd form-scratch
```

## Create readme file, add ignore file, init Git and make first commit

```
$ touch README.md
$ touch .gitignore
$ git init
$ git add .
$ git commit -m "initial commit"
```

## Init node project with package.json file

```
$ yarn init -y
```

## Add node modules

Add react packages to the project.

```
$ yarn add react react-dom
```

Setup webpack '-D' developer dependencies.

```
$ yarn add -D webpack webpack-cli webpack-dev-server html-webpack-plugin
```

Setup Babel '-D' developer dependencies.

```
$ yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader
$ yarn add -D @babel/plugin-proposal-class-properties
```

Setup styels sass & css.

```
$ yarn add -D css-loader sass-loader sass mini-css-extract-plugin
```

Setup for env variables.

```
$ yarn add env-cmd
```

# Configuration

## Create an HTML file inside src/ folder with the content

```
$ mkdir src && cd src && touch index.html
```

```
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />

        <title>Setup React Application From Scratch</title>
    </head>

    <body>
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <div id="root"></div>
    </body>
</html>
```

## Create a js file inside src/ folder.

```
$ touch index.js
```

```
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(<div> Hello World! </div>, document.getElementById("root"));
```

## Create js and .env file with configuration to easily import env variables

#### Environmet variables

```
$ touch .env.dev
```

```
NODE_ENV=development
PORT=9000
HOST=http://localhost

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=baconpancakes
DB_NAME=tree_fort
```

#### Configuration file

```
$ touch config.js
```

```
const config = {
    NODE_ENV: process.env.NODE_ENV,
    API_URL: `${process.env.HOST}:${process.env.PORT}`,
    HOST: process.env.HOST,
    PORT: process.env.PORT,
};

module.exports = config;
```

## In root of app create js file to put configure for webpack manager

```
$ touch webpack.config.js
```

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { PORT, NODE_ENV, API_URL } = require('./config');

module.exports = {
    entry: path.resolve(\_\_dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'public'),
        filename: 'assets/js/index.bundle.js',
        publicPath: '/',
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                include: path.resolve(__dirname, 'src'),
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env', '@babel/preset-react'],
                        plugins: ['@babel/plugin-proposal-class-properties'],
                    },
                },
            },
            {
                test: /\.css$/,
                use: [
                    {
                        loader: MiniCssExtractPlugin.loader,
                        options: {
                            hmr: process.env.NODE_ENV === 'development',
                        },
                    },
                    'css-loader',
                    'sass-loader',
                ],
            },
        ],
    },
    devServer: {
        contentBase: path.resolve(__dirname, 'public'),
        port: PORT,
        hot: true,
        historyApiFallback: true,
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: 'src/index.html', //source html
        }),
        new MiniCssExtractPlugin({
            filename: `assets/css/[name]-[hash].css`,
            chunkFilename: `assets/css/[id]-[hash].css`,
        }),
    ],

};
```

## Add the scripts to package.json file

```
{
    "scripts": {
        "dev": "env-cmd -f .env.dev webpack-dev-server",
        "prod": "env-cmd -f .env.prod webpack",
        "build": "env-cmd -f .env.prod webpack",
    }
}
```

## That's all! It's show time.

Let's start the development server.

```
yarn dev
```

Voila!!! We are done. Let's see the output.

```
http://localhost:9000
```
