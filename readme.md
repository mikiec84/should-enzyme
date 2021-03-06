# should-enzyme

[![npm version](https://img.shields.io/npm/v/should-enzyme.svg)](https://www.npmjs.com/package/should-enzyme)
[![Build Status](https://travis-ci.org/rkotze/should-enzyme.svg?branch=master)](https://travis-ci.org/rkotze/should-enzyme)

[should.js](https://shouldjs.github.io/) assertions for [enzyme](https://github.com/airbnb/enzyme)

1. [Install](#install)
1. [Setup](#setup)
1. [Assertions](#assertions)
1. [`attr(key, [value])`](#attrkey-value)
1. [`checked()`](#checked)
1. [`className(string)`](#classnamestring)
1. [`contain(node)`](#containnode)
1. [`containsText(string)`](#containstextstring)
1. [`data(key, [value])`](#datakey-value)
1. [`disabled()`](#disabled)
1. [`exactClassNames(string)`](#exactclassnamesstring)
1. [`present()`](#present)
1. [`prop(key, [value])`](#propkey-value)
1. [`props(object)`](#propsobject)
1. [`state(key, [value])`](#statekey-value)
1. [`text(string)`](#textstring)
1. [`value(string)`](#valuestring)
1. [Contribute](https://github.com/rkotze/should-enzyme/blob/master/CONTRIBUTING.md)

## Install

`npm i should-enzyme --save-dev`

## Setup

Install [Enzyme JS](https://github.com/airbnb/enzyme#installation)

```js
import "should";
import "should-enzyme";
```

## Assertions

### `attr(key, [value])`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if element has attribute and optionally check value.

```js
import { mount, render, shallow } from "enzyme";
import React, { PropTypes } from "react";

const AttrFixture = ({ children, title }) => <div title={title}>content</div>;

AttrFixture.propTypes = {
  children: PropTypes.node,
  title: PropTypes.string
};

const wrapper = mount(<AttrFeature />);

wrapper.should.have.attr("title");
wrapper.should.have.attr("title", "enzyme");
wrapper.should.not.have.attr("pizza");
wrapper.should.not.have.attr("title", "stuff");
```

### `checked()`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if input type checkbox is checked.

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const CheckedFixture = () => (
  <div>
    <input id="coffee" type="checkbox" defaultChecked value="coffee" />
    <input id="tea" type="checkbox" value="tea" />
  </div>
);

const wrapper = renderMethod(<CheckedFixture />);
const coffee = wrapper.find("#coffee");
const tea = wrapper.find("#tea");

coffee.should.checked();
tea.should.not.be.checked();
```

### `className(string)`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if wrapper has css class.

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const ClassNameFixture = () => (
  <div className="special burger">Content here</div>
);

const wrapper = mount(<ClassNameFixture />);

wrapper.should.have.className("special");
wrapper.should.not.have.className("pizza");
```

### `contain(node)`

| render | mount | shallow |
| ------ | ----- | ------- |
| no     | yes   | yes     |

Check to see if wrapper contains the expected node.

```js
import React from "react";
import { mount, shallow } from "enzyme";

const Banana = () => {
  return <div>Banana</div>;
};

const Apple = props => {
  return <div>Apple</div>;
};

const ContainNodesFixture = () => {
  return (
    <div>
      <Apple name="Jim" />
      <Apple name="Bob" />
    </div>
  );
};

const wrapper = mount(<ContainNodesFixture />);

wrapper.should.contain(<Apple name="Bob" />);
wrapper.should.not.be.contain(<Banana />);
```

### `containsText(string)`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if wrapper contains text.

```js
import React from 'react';
import {mount, render, shallow} from 'enzyme';

const TextFixture = () => (
  <div>Content here. More content</div>
);

cont wrapper = mount(<TextFixture />);

wrapper.should.containsText('Content here');
wrapper.should.not.containsText('pizza');
```

### `data(key, [value])`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if element has a data attribute and optionally check value.

```js
import { mount, render, shallow } from "enzyme";
import React, { PropTypes } from "react";

const DataFixture = ({ children, tr }) => (
  <div data-tr={tr} data-id="special-id">
    content
  </div>
);

DataFixture.propTypes = {
  children: PropTypes.node,
  tr: PropTypes.string
};

const wrapper = mount(<DataFixture tr="enzyme" />);

wrapper.should.have.data("tr");
wrapper.should.have.data("tr", "enzyme");
wrapper.should.not.have.data("pizza");
wrapper.should.not.have.data("tr", "stuff");
```

### `disabled()`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if input fields are disabled.

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const DisabledFixture = () => (
  <div>
    <input id="coffee" type="text" value="coffee" />
    <input id="tea" type="text" disabled value="tea" />
  </div>
);

const wrapper = renderMethod(<DisabledFixture />);
const coffee = wrapper.find("#coffee");
const tea = wrapper.find("#tea");

coffee.should.not.be.disabled();
tea.should.be.disabled();
```

### `exactClassNames(string)`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if wrapper has the exact class names.

```js
import React from 'react';
import {mount, render, shallow} from 'enzyme';

const ClassNamesFixture = () => (
  <div className="special buffalo chicken burger">Content here</div>
);

cont wrapper = mount(<ClassNamesFixture />);

wrapper.should.have.exactClassNames('special buffalo chicken burger');
wrapper.should.not.have.exactClassNames('special buffalo chicken');
wrapper.should.not.have.exactClassNames('other class names');
```

### `present()`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if the wrapper is present.

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const PresentFixture = () => (
  <div>
    <div id="burgers">with cheese</div>
    <div>side of fries</div>
  </div>
);

const wrapper = mount(<PresentFeature />);
const burgers = wrapper.find("#burgers");
const salad = wrapper.find("#salad");

burgers.should.be.present();
salad.should.not.be.present();
```

**Exception:** Using `render` only with Enzyme 3 means `null` components are not classed as "present".
This is related to the cheerio wrapper v1 being returned.

See example below:

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const PresentFixture = () => null;

const wrapperMount = mount(<PresentFeature />);
wrapperMount.should.be.present(); // true

const wrapperRender = render(<PresentFeature />);
wrapperRender.should.be.present(); // false
```

### `prop(key, [value])`

| render | mount | shallow |
| ------ | ----- | ------- |
| no     | yes   | yes     |

Check to see if wrapper has prop and optionally check value.

```js
import React from "react";
import { mount, shallow } from "enzyme";

const PropFixture = ({ children, id, myObj }) => <div id={id}>salad</div>;

const wrapper = mount(<PropFeature id="mango" myObj={{ foo: "bar" }} />);

wrapper.should.have.prop("id");
wrapper.should.not.have.prop("iDontExistProp");

wrapper.should.have.prop("id", "mango");
wrapper.should.not.have.prop("id", "banana");
// assert objects
wrapper.should.have.prop("myObj", { foo: "bar" });

wrapper.should.not.have.prop("iDontExistProp", "banana");
```

### `props(object)`

| render | mount | shallow |
| ------ | ----- | ------- |
| no     | yes   | yes     |

Check to see if wrapper has props and value. This uses shouldJS `deepEqual` assert.

```js
import React from "react";
import { mount, shallow } from "enzyme";

const PropsFixture = ({ id, title, total }) => (
  <div id={id} title={title} total={total}>
    content
  </div>
);

const wrapper = mount(
  <PropsFixture id="content" title="superfood" total={24} />
);

wrapper.should.have.props({ id: "content" });
wrapper.should.have.props({ id: "content", title: "superfood", total: 24 });

wrapper.should.not.have.props({ food: "pizza" });
wrapper.should.not.have.props({ id: "stuff" });

wrapper.should.have.props(); // will error require object
```

### `state(key, [value])`

| render | mount | shallow |
| ------ | ----- | ------- |
| no     | yes   | yes     |

Check to see if wrapper has state property and optionally check value.

```js
import React, { Component } from "react";
import { mount, shallow } from "enzyme";

class StateFixture extends Component {
  constructor() {
    super();
    this.state = {
      bestFruit: "mango"
    };
  }

  render() {
    return <div id="best-mangos">{this.state.bestFruit}</div>;
  }
}

const wrapper = mount(<StateFeature />);

wrapper.should.have.state("bestFruit");
wrapper.should.not.have.state("anotherFruit");

wrapper.should.have.state("bestFruit", "mango");
wrapper.should.not.have.state("bestFruit", "orange");

wrapper.should.not.have.state("anotherFruit", "banana");
```

### `text(string)`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Check to see if the exact text content is in wrapper.

```js
import React from 'react';
import {mount, render, shallow} from 'enzyme';

const TextFeature (props) => (
      <div id='text-feature'>
        <span id='text-span'>Test</span>
      </div>
    );

const wrapper = mount(<TextFeature />);

wrapper.find('#text-span').should.have.text('Test');

wrapper.find('#text-span').should.not.have.text('Other text');
```

### `value(string)`

| render | mount | shallow |
| ------ | ----- | ------- |
| yes    | yes   | yes     |

Assert on input field values this includes `<input>`, `<select>` and `<textarea>`.

```js
import React from "react";
import { mount, render, shallow } from "enzyme";

const FormInputsFixture = () => (
  <form>
    <input type="text" name="mug" defaultValue="coffee" />
    <select defaultValue="pizza">
      <option value="coffee">More coffee</option>
      <option value="pizza">Pizza</option>
      <option value="salad">Salad</option>
    </select>
    <textarea name="fruit" value="Hands or bunch of bananas?" />
    <div id="failSelect">What value?</div>
  </form>
);

const wrapper = mount(<FormInputsFixture />);

wrapper.find("input").should.have.value("coffee");
wrapper.find("input").should.not.have.value("pizza");

wrapper.find("select").should.have.value("pizza");
wrapper.find("select").should.not.have.value("salad");

wrapper.find("textarea").should.have.value("Hands or bunch of bananas?");
wrapper.find("textarea").should.not.have.value("Mangoes");
```
