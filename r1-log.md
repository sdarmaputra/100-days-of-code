# #100DaysOfCode Log - Round 1 - [@sdarmaputra](https://github.com/sdarmaputra)

The log of my #100DaysOfCode challenge. Started on [February 12, Monday, 2018].

## Log

### R1D1 (February 12, 2018) :dolphin:
**Progress:**
- Uploading my on going timer project to GitHub
- Integrating it with Travis CI
- Experimenting Javascript Object.defineProperty() to listen for variable changes 
- Create a simple count-down app in [Codepen](https://codepen.io)

**Lesson Learned:**
- We can listen to the changes of object property using Object.defineProperty() method. It can be done like this:
```
Object.defineProperty(component, 'props', {
    get() {
      return 'something'
    },
    set(newProps) {
      component._props = newProps
      console.log('props changes')
      // execute an action if props changes
    }
  })
```
- Javascript Object has a lot of cool properties that I need to learn more.

**Link(s) to Work:**
- [Object.defineProperty() Experiment](https://codepen.io/sdarmaputra/pen/GQEgVP/)
- [On Going Timer App](https://github.com/sdarmaputra/simple-timer)

### R1D2 (February 14, 2018) :dolphin:
**Progress:**
- Experimenting Javascript Object

**Lesson Learned:**
- We can define property getter and setter in both way:
```
Object.defineProperty(component, 'props', {
    get() {
      // return props
    },
    set(newProps) {
      // set props
    }
  })
```
or
```
const component = {
    _props: {},
    get props() {
        return this._props
    },
    set props(newValue) {
        this._props = newValue
    }
}
```
- If we only define getter then the property cannot be set, vice versa
- A property without getter returns `undefined`

**Link(s) to Work:**
- [https://repl.it/@sdarmaputra/Object-Playground](https://repl.it/@sdarmaputra/Object-Playground)


### R1D3 (February 15, 2018) :hamster:
**Progress:**
- Uploading new project to solve a challenge from WWWID: [https://medium.com/wwwid/tantangan-web-developer-untuk-membuat-aplikasi-web-bisa-digunakan-kurang-dari-5-detik-70bb7431741d](https://medium.com/wwwid/tantangan-web-developer-untuk-membuat-aplikasi-web-bisa-digunakan-kurang-dari-5-detik-70bb7431741d)
- Integrating it with Travis CI
- Create several components
- Practicing test-first approach for development

**Lesson Learned:**
- At the first time to learn TDD, it's hard to start writing test first before writing our real code because sometimes we doubt whether our test is valid or not
- But, if we can handle it, we have a bunch of cool things that can automagically verify whether our code have met the specification or not
- I found out using jasmine as a test framework for Javascript project is easier than mocha because it already have assertion library and mocking function
- But, if we prefer more flexible solution, mocha is a good choice
- Setting up jasmine is simple:
    - install jasmine (`yarn add --dev jasmine`)
    - run `jasmine init`
    - it will create `spec` directory which you can place your tests in
    - create test file with `*.spec.js` as a file name
    - run `jasmine` and see your test success or fail
- We can set up browser-like environment using JSDOM and jasmine helpers:
    - install JSDOM (`yarn add --dev jsdom`)
    - create `environment.js` inside directory `spec/helpers`
    - write these codes into `environment.js`:
    ```
    const { JSDOM } = require('jsdom')

    const page = new JSDOM('<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Awesome Test</title></head><body></body></html>')
    const { window } = page
    const { document, Element } = window

    global.window = window
    global.document = document
    global.Element = Element //this is optional
    ```
    - Above code attempts to append `window` and `document` object as we have in common browsers to Node.js global variable so we can access both of them using `window` and `document` inside our tests. By default, Node.js doesn't provide `window` and `document`, so if we try to use them without any help from JSDOM, we will get `undefined` object instead.
    - verify jasmine helpers is pointed to `spec/helpers` directory, here is my jasmine configurations:
    ```
    {
      "spec_dir": "spec",
      "spec_files": [
        "**/*[sS]pec.js"
      ],
      "helpers": [
        "helpers/**/*.js"
      ],
      "stopSpecOnExpectationFailure": false,
      "random": false
    }
    ```
    - We can find jasmine configurations inside file `spec/support/jasmine.json`. Configurations above is the default jasmine configurations
- Be carefull to use jasmine 3.x because at the moment I wrote this log, it still unstable I think. When our test fail, it didn't show any error messages. Therefore I downgraded my project to use jasmine 2.9

**Link(s) to Work:**
- https://github.com/sdarmaputra/wwwid-feed


### R1D4 (February 16, 2018) :monkey:
**Progress:**
- Refactoring [WWWID Feed](https://github.com/sdarmaputra/wwwid-feed)
- Trying to separate components to make the code clearer and easy to understand
- Creating styles using SASS
- Generate HTML page using `html-webpack-plugin`
- Extracting CSS into  a separated file using `extract-text-webpack-plugin`

**Lesson Learned:**
- Using component-based architecture for front-end project make our code clearer and easier to maintain and understand
- But, sometimes if we do inappropriate separation, we can mess up our project structure and make our code more confusing to follow
- It's fine to write a very long component code at the first time because sometimes we haven't realized if that component needs to be separated or not. We need to iterate several times to find the best separation strategy for our components. Again, writing test first helps us to keep our code on track and won't mess anything up.
- Sometimes `webpack-dev-server` failed to use Hot Module Replacement (HMR) and I haven't found the causes yet. But, some folks suggest to start up `webpack-dev-server` like this `webpack-dev-server --hot --inline` **rather than** using this code inside webpack configuration:
    ```
    devServer: {
        //some configs
        hot: true
    }
    ```

**Link(s) to Work:**
- https://github.com/sdarmaputra/wwwid-feed


### R1D5 (February 17, 2018)
**Progress:**
- Experimenting with `window.location` and `RegEx`

**Lesson Learned:**
- We can use `location.hash` to obtain hash URL
- We can make use of this location hash to build custom routing mechanism for our Single Page App
- Using `RegEx` to process our URL and redirect into the right component is pretty awesome
- Here's some `RegEx` pattern that I found usefull: `/{(.*?)}/g` to find all string inside curly braces (both curly braces included). We can use this pattern for example to find parameter name within a URL pattern like this `url/{param1}/{param2}`
 
 **Link(s) to Work:**
- https://github.com/sdarmaputra/wwwid-feed

### R1D6 (February 18, 2018)
**Progress:**
- Separate my custom routing mechanism into a reusable module
- More experiments with `RegEx`
- Finishing basic app flow of [WWWID Reader](https://github.com/sdarmaputra/wwwid-feed)

**Lesson Learned:**
- JSDOM haven't implemented `scrollTo` function yet,  so I have to hack it a bit to hide it's error message saying that function hasn't implement yet. Here's what I've done so far :sweat_smile: :
```
global.window.scrollTo = () => ({  })
```
- If we want to create an object that can listen to its property changes, we have to duplicate all of the properties into something else then define setter and getter. For example, I have a `store` object and I want to listen for property changes. So I copy all property into \_property, then define new property that accesses \_property:
```
Object.keys(store).map(key => {
    store['_'+key] = store[key]
    Object.defineProperty(store, key, {
        get: function() {
            console.log('get '+key)
            return this['_'+key]
        },
        set: function(value) {
            console.log('update '+key)
            this['_'+key] = value
            processChange()
        }
    })
})

```
- Several usefull CSS styles to beautify our `<pre>` tag:
```
pre {
    background: #efefef;
    margin: 0;
    margin-block-start: 0;
    margin-block-end: 0;
    padding: $baseline * 0.3 $baseline;
    white-space: pre-wrap;
    word-wrap: break-word;
}
```
- Using `word-wrap: break-word;` inside our element is sometimes usefull, for example when we have a very long URL that overflows our element, we can break that long string and wrap it into new line

 **Link(s) to Work:**
- https://github.com/sdarmaputra/wwwid-feed


### R1DX (MM DD, 2018)
**Progress:**
- Do semething

**Lesson Learned:**
- Something awesome

**Link(s) to Work:**
- Something aweseome
