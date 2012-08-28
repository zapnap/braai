# Braai

A fully extensible templating system. Sick and tired of all of those templating systems that force you to do things their way? Yeah, me too! Thankfully there's Braai. 
Braai let's you write your own Regular Expression matchers and then do whatever you'd like when the template is parsed! Sounds fun, doesn't it?

## Installation

Add this line to your application's Gemfile:

    gem 'braai'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install braai

## Usage

### Built-in Matchers

Braai comes shipped with two simple matchers for you, but you can easily add your own.

The first matcher is a simple <code>to_s</code> handler. It will match a single variable and then call <code>to_s</code> on it:

<pre><code>
template = "Hi {{ name }}!"
response = Braai::Template.new(template).render(name: "Mark")
response # => "Hi Mark!"
</code></pre>

The second matcher will call a method on the variable.

<pre><code>
template = "Hi {{ name.upcase }}!"
response = Braai::Template.new(template).render(name: "Mark")
response # => "Hi MARK!"
</code></pre>

### Custom Matchers

Braai let's you easily define your own matchers to do whatever you would like to do.

<pre><code>
template = "I'm {{ name }} and {{ mmm... bbq }}!"
Braai::Template.map(/mmm\.\.\. bbq/i) do |template, key, matches|
  "Damn, I love BBQ!"
end

Braai::Template.map(/name/i) do |template, key, matches|
  template.attributes[matches.first].upcase
end

Braai::Template.new(template).render # => "I'm MARK and Damn, I love BBQ!!"
</code></pre>

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
