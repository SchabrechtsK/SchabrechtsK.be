---
title: Twig Params as Twig Path() params
author: Kenneth
type: post
date: 2017-08-13T00:00:00+00:00
url: /development/twig-params-as-twig-path-params/
featured_image: /wp-content/uploads/2017/08/1XubqkYXDtHE0bDNYnAmsuA.jpeg
categories:
  - Development
tags: []

---
When our current project started we were tasked to create a BaseCrudController. Since we were going to use a lot of basic CRUD actions in the beginning of the project.

Setting up the entire BaseCrudController was not that much of an issue. Except for one small hick-up. When extending this BaseCrudController you would not know what parameter was needed to pass an entity id on to the next view. For example when you wanted to create a view or edit action.

So we were forced to set this parameter name through an abstract function. The endcontroller would look something like the following code example. We’re just displaying the view action here to keep it short and sweet.

<pre class="wp-block-code"><code>&lt;?php
namespace AppBundle\Controller;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;
class TwigParamExampleController extends Controller
{ 
  /**
     * @param Request $request
     * @param $entityId
     * @return string
     */
    public function viewAction(Request $request, $entityId)
    {
        $entity = $this->getRepository()->find($entityId);
        return $this->render($this->getDetailView(), [
            'edit_url' => $this->getEditPathName(),
            'twig_param_name' => $this->getTwigParamName(),
            'entity' => $entity
        ]);
    }
}</code></pre>

If you look at the code you can see we used multiple abstract methods to set-up the endcontroller. In this way we could setup a new CRUD controller fast and with ease. All we had to do was implement the abstracted functions.

For the render in this example we first define the detail view, which is the twig file that should be rendered. The next part is the edit url used in the path so we can navigate to the correct action. The third part is the parameter name for Twig to use in that path. Lastly we would pass the entity itself so it can be displayed in the view.

Our first instinct was to use the _twig\_param\_name_ in the same way we use any parameter as shown in the next example.

<pre class="wp-block-code"><code>&lt;a href="{{ path(edit_url, {twig_param_name: entity.id}) }}">Link&lt;/a></code></pre>

Needles to say, this would throw an error. And so we went on to search for a working solution.

The solution we found was actually very simple. All we had to do was to let Twig know that this was actually a parameter. The way we can do this is by surrounding the twig\_param\_name parameter with parentheses. This is shown in the next example.

<pre class="wp-block-code"><code>&lt;a href="{{ path(edit_url, {(twig_param_name): entity.id}) }}">Link&lt;/a></code></pre>

And just like that we had our BaseCrudController figured out with it’s own views and working links.