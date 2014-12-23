# CakePHP (2.x) Mustache Plugin
Mustache View helper (*originally CakePan*) that renders Mustache templates. It will also load and process partials!

### Why use Mustache templates in CakePHP?
<strong>Portability and scalability!</strong> If you have an app that uses lots of front-end coding, you only have to write your templates once. Mustache templates can be rendered in PHP, Javascript, Ruby, Scala, even C++! If you want to move to or from some other framework (Rails, Grails, Lithium etc.), you can be sure that your views and design won't have to be re-built.

For scalability, when the time comes, you can use templates with a more powerful engine like Scala, or just send JSON from any source, and render with Javascript. 

## Installation

### 1. From app directory - `git submodule add https://github.com/electblake/CakePHP-Mustache-Plugin.git Plugin/Mustache`
### 2. cd into Plugin/Mustache (so we can pull in the latest php implementation of mustache into Plugin/Mustache/Vendor)
### 3. `git submodule init`
### 4. `git submodule update`


If you want to add Mustache support globally, add it to your `AppController`

	class AppController extends Controller {
		...
		public $helpers = array('Mustache.Mustache');
		...
	}

## Usage

See the Mustache manual: [http://mustache.github.com/](http://mustache.github.com/)

### Creating a Mustache Template

Your Mustache templates should all be in the `/app/View/Elements/` directory, with a `.mustache` extension.

/app/View/Elements/post.mustache

	{{#Post}}
	<h2>{{title}}</h2\>
	<div>
		{{text}}
	</div>
	{{/Post}}


### Rendering a Mustache Template

All the variable set by the controller are available, and merged with values passed into `$params`.

	$params = array(
		'title' => 'Show me the bacon!',
		'text' => 'Bacon ipsum dolor sit amet fatback pig swine...'
	);

	$this->Mustache->render('template_name', $params)



### Using Partials

Partials should follow the same naming convention. Mustache will pass the variables to the partial in the context that it's called. For example, a nested template for a blog `post` with `comments` might look like:

/app/View/Elements/posts/post.mustache:

	{{#Post}}
	<h2>{{title}}</h2\>
	<div>
		{{text}}
	</div>
	{{/Post}}
	{{#Comment}}
		{{>post/comment}}
	{{/Comment}}

/app/View/Elements/posts/comment.mustache:

	<div>
	<h3>{{#User}}{{name}}{{/User}} said: </h3>
	<p>{{text}}</p>
	</div>
