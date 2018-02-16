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
