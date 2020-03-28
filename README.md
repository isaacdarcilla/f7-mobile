## ✨ Desktop Query

<p align="center"><img src="https://cdn.framework7.io/i/logo-text-red.svg" width="400"></p>

<p align="center">🎉 Desktop query application powered by Framework7 and Vue built with</p>

<p align="center"><img src="https://onsenui.github.io/art/logos/monaca-logo-2.png" width="200"></p>

## Installation

* `git clone https://github.com/isaacdarcilla/f7-mobile.git` - clone the repository
* `cd f7-mobile` - change to project directory
* `npm install` - install npm package
* `npm start` - run development server
* `npm run build-prod` - build web app for production
* `npm run build-dev` - build web app using development mode (faster build without minification and optimization)

## Importing project to Monaca

* [Importing Projects On Github with Monaca](https://docs.monaca.io/en/products_guide/monaca_ide/version_control/github_integration/)

## API Endpoints

* `GET` - Fetch all desktop.
* `URL` - https://querybackend.herokuapp.com/fetch-desktops.php
* `PARAM` - None

```yaml
[
  {
    "id": "25",
    "archived": "0",
    "desktopname": "DSKTP-MIS04",
    "location": "Management Information Services",
    "model": "Dell",
    "updatedon": "November 09, 2019",
    "frequency": "Twice",
    
    ...
  }
]
```

* `GET` - Fetch desktop by name.
* `URL` - https://querybackend.herokuapp.com/fetch-desktops-by-name.php?desktopname=DSKTP-CE10
* `PARAM` - desktopname

```yaml
[
  {
    "id": "10",
    "archived": "1",
    "desktopname": "DSKTP-CE10",
    "location": "Office Of The College Of Engineering",
    "model": "Dell",
    "updatedon": "January 09, 2020",
    "frequency": "No data available",
    
    ...
  }
]
```

## Screenshot

More screenshot can be found in ```screenshot``` folder.

Home Tab  | Desktop Tab
------------- | -------------
![App](https://github.com/isaacdarcilla/f7-mobile/blob/master/screenshot/_home_isaac_Desktop_Dev_Vue_desktop-vue_www_index.html%20(2).png?raw=true) | ![App](https://github.com/isaacdarcilla/f7-mobile/blob/master/screenshot/_home_isaac_Desktop_Dev_Vue_desktop-vue_www_index.html%20(3).png)

## License

[Apache 2.0 License](https://github.com/isaacdarcilla/DesktopQuery/blob/master/LICENSE)

## WebPack

There is a webpack bundler setup. It compiles and bundles all "front-end" resources. You should work only with files located in `/src` folder. Webpack config located in `build/webpack.config.js`.

Webpack has specific way of handling static assets (CSS files, images, audios). You can learn more about correct way of doing things on [official webpack documentation](https://webpack.js.org/guides/asset-management/).
