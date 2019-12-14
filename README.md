# Bootstrap and Font Awesome 5 with Rails 6 and Webpacker 

> This README is above all a cheatsheet made for me and by me. It may not suit your needs.

## Installation

- Create a new Rails 6 project (optional):
```bash
rails new bootstrap-app
```

### Bootstrap

- Inside, install Bootstrap, jQuery and Popper.js:
```bash
yarn add bootstrap jquery popper.js
```

- In `app/javascript/`, create a `stylesheets/` directory and inside it, a `application.scss` file. In `application.scss`:

```scss
@import "~bootstrap/scss/bootstrap";
```

- In `app/javascript/packs/application.js`, import the scss file:

```js
import 'bootstrap/dist/js/bootstrap';
import '../stylesheets/application.scss';
```

- In `app/views/layouts/application.html.erb`, replace "stylesheet_link_tag" by "stylesheet_pack_tag":

```erb
  <%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
```

- In `config/webpacker.yml`, set default value of `extract_css:` key to `true`:

```yml
# Extract and emit a css file
  extract_css : true
```

- In `config/webpack/environment.js`, require webpack:

```js
const { environment } = require('@rails/webpacker')

const webpack = require('webpack');
environment.plugins.append(
  'Provide',
  new webpack.ProvidePlugin({
    $: 'jquery',
    jQuery: 'jquery',
    Popper: ['popper.js', 'default'],
  }),
);

module.exports = environment
```

- Run `rails server` and `bin/webpack-dev-server` commands in two different terminal windows.

### Font Awesome 5 (free)

- Install Font Awesome by running:
```bash
yarn add @fortawesome/fontawesome-free
```

- In `Gemfile`, add [font_awesome5_rails](https://github.com/tomkra/font_awesome5_rails) gem and run `bundle install`:
```rb
gem 'font_awesome5_rails', '~> 0.9.0'
```

This gem offers view helpers like:
```erb
<%= fa_icon 'camera-retro' %>
```

- In `app/javascript/stylesheets/application.scss`:

```scss
@import "~bootstrap/scss/bootstrap";
@import "~@fortawesome/fontawesome-free";
```

- In `app/javascript/packs/application.js`:

```js
import 'bootstrap/dist/js/bootstrap';
import '@fortawesome/fontawesome-free/js/all';
import '../stylesheets/application.scss';
```

And you are done! You may have to rerun `rails server` and/or `bin/webpack-dev-server` sometimes.
