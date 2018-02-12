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
