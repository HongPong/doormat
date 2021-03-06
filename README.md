![img](https://img.shields.io/badge/license-MIT-blue.svg)
![img](https://img.shields.io/badge/dependencies-none-green.svg)

# doormat
_an alternative way to navigate through your site content_

![alt tag](https://raw.github.com/jh3y/pics/master/doormat/doormat.jpg)

`doormat` provides a slightly different way to traverse through your site content.

## Usage

To create your doormat.

1. Include `doormat{.min}.js` and `doormat{.min}.css` in your page.

2. Create your DOM structure. The structure needs to be a container with the classname `dm`. It then needs to have children with the classname `dm__pnl`. `ol` and `ul` are fitting elements.

  ```html̨
    <ol class="dm">
      <li class="dm__pnl">Awesome</li>
      <li class="dm__pnl">Site</li>
      <li class="dm__pnl">Content</li>
    </ol>
  ```

3. Invoke the `Doormat` function passing in desired options (_explained below_) as a parameter. Note this must run _after_ the object exists in the DOM (thus it won't work in the head).

  ```javascript
  var myDoormat = new Doormat();
  var myDoormat = new Doormat({
    scrollBuffer : 15,
    snapDuration : 250,
    snapThreshold: 15
  });
  ```

## API options
* `scrollBuffer {number}` - The `scrollBuffer` represents a vertical percentage of `window.innerHeight` to be used as a buffer delay when triggering the next doormat panel to scroll. For example; If my `window` was `1000px` high and I set the `scrollBuffer` as `10`, the scrolling buffer would be `100px`. The reason for percentage is that when the window is resized the delay will remain consistent and proportional to the `window` height.
* `snapThreshold {number}` - The `snapThreshold` works in a similar way to `scrollBuffer` in that it translates to a percentage of `window.innerHeight`. It is used so that the closest panel edge will snap to the viewport when we are scrolling within the defined `snapThreshold`.
* `snapDuration {number}` - The `snapDuration` defines the length of time that are snap functionality is debounced and also the amount of time it will take for our panels to snap to viewport. The `snapDuration` is defined in `ms`. For example; `250`.

## How?
The trick is possible by making sections of the page `position: fixed` and then setting a height for the document `body` equal to the combined height of the page sections.

When the `window` is scrolled down we move our page sections upwards out of the viewport to reveal the content underneath. The opposite being that, when the `window` is scrolled up, we bring our sections back down into view in the same order in which they left(_dictated by the DOM structure_).

## curtain.js?
Unfortunately, `curtain.js` is no longer maintained and there were reports of issues with newer versions of jQuery.

`curtain.js` is a more feature rich solution and provides some different behavior and hooks. It does however depend on `jQuery`.

I was unaware of `curtain.js` when creating `doormat`. Initially, I was experimenting with different implementations of parallax style effects and messing about with viewport units.

My aim with `doormat` was to create the effect but keep the solution minimal with no dependencies. It was a result of curiosity and playing with code.

## Development
If you wish to play with the code, it's simple to get going.

1. Fork and clone or simply clone the repo.

        git clone https://github.com/jh3y/doormat.git

2. Navigate into the repo and install the dependencies.

        cd doormat
        npm setup

3. Run the `develop` task to get up and running with `browser-sync` etc.

        npm run develop

__NOTE::__ I would usually use a task runner like `gulp` in my projects. But, with `doormat` being minimal I had a go at using `npm run scripts` for all my build needs. So, to see all available build scripts, take a look at `package.json`.
```shell
npm run
```
### Roll your own
`doormat` development is mainly config driven with `doormat.config.json`. In here you can alter the classnames for elements to your desire. It is __important__ to remember that if you change the classnames in the config though that you will also need to update any reference to them from within the JavaScript.

For example, maybe you're not keen on the classnames being used or want it to support a higher number of panels(_the default is 10_).

Change the config and then run the build task with `npm run publish`.

## Contributing
Don't hesitate to post an issue or suggestion or get in touch by tweeting me [@_jh3y](https://twitter.com/_jh3y)!

## License
MIT

jh3y 2016
