*This repository is a mirror of the [component](http://component.io) module [yyx990803/speech](http://github.com/yyx990803/speech). It has been modified to work with NPM+Browserify. You can install it using the command `npm install npmcomponent/yyx990803-speech`. Please do not open issues or send pull requests against this repo. If you have issues with this repo, report it to [npmcomponent](https://github.com/airportyh/npmcomponent).*
# Speech

Simple wrapper for Chrome's web speech recoginition API.

<a href="http://sketch.evanyou.me/speech/" target="_blank">Demo</a>

### Basic Usage

``` js

var Speech = require('speech')
var recognizer = new Speech({
    lang: 'cmn-Hans-CN', // Mandarin Chinese, default is English.
    // all boolean options default to false
    debugging: true, // will console.log all results
    continuous: true, // will not stop after one sentence
    interimResults: true, // trigger events on iterim results
    autoRestart: true, // recommended when using continuous:true
                      // because the API sometimes stops itself
                      // possibly due to network error.
})

// simply listen to events
// chainable API
recognizer
    .on('start', function () {
        console.log('started')
    })
    .on('end', function () {
        console.log('ended')
    })
    .on('error', function (event) {
        console.log(event.error)
    })
    .on('interimResult', function (msg) {
        document.body.innerHTML = msg
    })
    .on('finalResult', function (msg) {
        document.body.innerHTML = msg
    })
    .start()

```

You can also access Chrome's native recognition object:

``` js
recognizer.recognition.continuous = false
```

### Language Options

``` js

// from http://www.google.com/intl/en/chrome/demos/speech.html
var langs =
    [['Afrikaans',       ['af-ZA']],
     ['Bahasa Indonesia',['id-ID']],
     ['Bahasa Melayu',   ['ms-MY']],
     ['Català',          ['ca-ES']],
     ['Čeština',         ['cs-CZ']],
     ['Deutsch',         ['de-DE']],
     ['English',         ['en-AU', 'Australia'],
                         ['en-CA', 'Canada'],
                         ['en-IN', 'India'],
                         ['en-NZ', 'New Zealand'],
                         ['en-ZA', 'South Africa'],
                         ['en-GB', 'United Kingdom'],
                         ['en-US', 'United States']],
     ['Español',         ['es-AR', 'Argentina'],
                         ['es-BO', 'Bolivia'],
                         ['es-CL', 'Chile'],
                         ['es-CO', 'Colombia'],
                         ['es-CR', 'Costa Rica'],
                         ['es-EC', 'Ecuador'],
                         ['es-SV', 'El Salvador'],
                         ['es-ES', 'España'],
                         ['es-US', 'Estados Unidos'],
                         ['es-GT', 'Guatemala'],
                         ['es-HN', 'Honduras'],
                         ['es-MX', 'México'],
                         ['es-NI', 'Nicaragua'],
                         ['es-PA', 'Panamá'],
                         ['es-PY', 'Paraguay'],
                         ['es-PE', 'Perú'],
                         ['es-PR', 'Puerto Rico'],
                         ['es-DO', 'República Dominicana'],
                         ['es-UY', 'Uruguay'],
                         ['es-VE', 'Venezuela']],
     ['Euskara',         ['eu-ES']],
     ['Français',        ['fr-FR']],
     ['Galego',          ['gl-ES']],
     ['Hrvatski',        ['hr_HR']],
     ['IsiZulu',         ['zu-ZA']],
     ['Íslenska',        ['is-IS']],
     ['Italiano',        ['it-IT', 'Italia'],
                         ['it-CH', 'Svizzera']],
     ['Magyar',          ['hu-HU']],
     ['Nederlands',      ['nl-NL']],
     ['Norsk bokmål',    ['nb-NO']],
     ['Polski',          ['pl-PL']],
     ['Português',       ['pt-BR', 'Brasil'],
                         ['pt-PT', 'Portugal']],
     ['Română',          ['ro-RO']],
     ['Slovenčina',      ['sk-SK']],
     ['Suomi',           ['fi-FI']],
     ['Svenska',         ['sv-SE']],
     ['Türkçe',          ['tr-TR']],
     ['български',       ['bg-BG']],
     ['Pусский',         ['ru-RU']],
     ['Српски',          ['sr-RS']],
     ['한국어',            ['ko-KR']],
     ['中文',             ['cmn-Hans-CN', '普通话 (中国大陆)'],
                         ['cmn-Hans-HK', '普通话 (香港)'],
                         ['cmn-Hant-TW', '中文 (台灣)'],
                         ['yue-Hant-HK', '粵語 (香港)']],
     ['日本語',           ['ja-JP']],
     ['Lingua latīna',   ['la']]];

 ```