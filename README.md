# Neos - Simple Template for Fluid template path mapping

You never need to manually define a template path to your Fluid file anymore. The simple template automatically sets up folder paths based on the Neos best practises.

## Usage

1. Install with `composer require codeq/unicodenormalizer`

2. Your node types will automatically use the new template, examples of the auto mapping can be found below.

3. To use auto mapping in your Fusion components, the prototype needs to be baed on the SimplteTempalte
    ```
    prototype(Example.Site:Component.Footer) < prototype(CodeQ.SimpleTemplate:Template) {
   	  ...
   	}
    ```

## Best practises for folder and file naming

### NodeTypes
1. Each NodeType configuration has it’s own file:
   `Configuration/NodeTypes.<Document/Content>.<NodeType Name>.yaml`

2. Each NodeType has it’s own folder for rendering with:
	```
	Resources/Private/Fusion/<Document/Content>/<NodeType Name>/
	   <NodeType Name>.fusion 
	   <NodeType Name>.html (optional)
	```
3. The Fusion prototype name is
	`Example.Site:<Document/Content>.<NodeType Name>`

### Sub-NodeTypes
Some NodeTypes are only allowed inside other NodeTypes, e.g. a SliderItem is always a subnode of a Slider. To better group them you can use the following folder structure:

1. Each Sub-NodeType configuration has it’s own file:
    `Configuration/NodeTypes.<Document/Content>.<NodeType Name>.<Sub-NodeType Name>.yaml`

2. Each Sub-NodeType has it’s own folder for rendering with:
	```
	Resources/Private/Fusion/<Document/Content>/<NodeType Name>/<Sub-NodeType Name>/
	   <Sub-NodeType Name>.fusion
	   <Sub-NodeType Name>.html (optional)
	```

3. The Fusion prototype name is 
	`Example.Site:<Document/Content>.<NodeType Name>.<Sub-NodeType Name>`


### Standalone Fusion Components

Components are reusable Fusion (and Fluid) modules which can be reused when rendering different NodeTypes. A component consists of one Fusion and an optional Fluid file.

1. Each component has its own folder inside the Components folder with:
	```
	Resources/Private/Fusion/Components/<Component Name>/
	   <Component Name>.fusion 
	   <Component Name>.html (optional)
	```
2. Each Fluid component must inherit from `prototype(Example.Site:SimpleTemplate)`

3. The Fusion prototype name is
	`Example.Site:Component.<Component Name>`

## The main idea behind all of it is this: 
The location of all files related to a Fusion object (Fusion protype, Fluid template) should always be deducible from object's name name. E.g. 
```
Example.Site:Content.Slider   -> ../Private/Fusion/Content/Slider/Slider.fusion
                              -> ../Private/Fusion/Content/Slider/Slider.html
Example.Site:Component.Footer -> ../Private/Fusion/Component/Footer/Footer.fusion
                              -> ../Private/Fusion/Component/Footer/Footer.html
```

Certain prototypes should provide reusable functionality and therefore only named Components. Those should not bound to a particular NodeType. 

If you need to break apart one big Fusion prototype into a few smaller ones, you can always group them with another layer of namespacing, e.g.:
```
Example.Site:Content.News                 -> ../Private/Fusion/Content/News/News.fusion
Example.Site:Content.News.RelatedArticles -> ../Private/Fusion/Content/News/RelatedArticles/RelatedArticles.fusion
```
