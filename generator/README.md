#StoryGraph World Generator

The StoryGraph world generator is a program that translates a plain english description of a StoryGraph world into a working StoryGraph program. StoryGraph objects, especially rules, can be cumbersome to write out by hand, so this program allows you to easily define the basic types, rules and actors of your world and generate the code automatically. The program generated by the World Generator will be somewhat dull, but since the boilerplate is all there it will be easy to go in and make modifications and additions to add color to your StoryGraph world.

##How to Use

First, write a description of your world using the grammar below and save it to disk. Go to the root director of StoryGraph in your console and use the following command:
```shell
node generateWorld path/to/description.txt myWorld.js
```
The second parameter is the output file name and it is important that is has a .js extension. Now you can modify your world as you see fit. Generated worlds automatically console.log a four step story so you can immediately test you world like this:
```shell
node myWorld.js
```

##Grammar

Here is the grammar of the world generator. Note that the formats provided here are not flexible. Only the parts inside curly braces may be replaced with your custom text.

###Basic Types

FORMAT: There is a type called {typename}.  
EXAMPLE:
```code
There is a type called person. There is a type called ghost.
```

###Type Extensions

FORMAT: A {new type} is a {base type}.  
EXAMPLE:
```code
A woman is a person. A cat is an animal. A skeleton is a ghost.
```

###Type Decorators

FORMAT: Some actors are {typename}.  
OPTIONAL FORMAT: Some actors are {type one} and some are {type two}.  
EXAMPLE:
```code
Some actors are smart and some are stupid. Some actors are scary.
```

###Actors

Note that the placeholder {type} here may be a basic type or extended type preceded by any number of type decorators. See the example for clarification.

FORMAT: There is a {type} called {name}.  
EXAMPLE:
```code
There is a ghost called Slimer. There is a smart kind man named Joe. There is a beautiful woman named Angelina.
```

###Rules

Again, the placeholder {type} may be preceded by any number of decorators.

FORMAT: If a {type one} <{encounter text}> a {type two} then the {type one||two} <{result text}>.  
OPTIONAL FORMAT: If a {type one} <{encounter text}> a {type two} then the {type one||two} <{result text}> the {type one||two}  
EXAMPLE:
```code
If a boy <is startled by> a ghost then the boy <starts to cry>. If a man <sees> a ghost then the man <stares in disbelief at> the ghost.
```

###Full Example
Here is a full working example:
```code
There is a type called entity. A vapor is an entity. A life is an entity.
An animal is a life. A solid is an entity.

Some actors are light and some are heavy. Some actors are wet and some are dry. Some actors are slow and some are fast. Some actors are bright and some are dark. Some actors are expansive and some are small.

A rock is a dry heavy solid. A bird is a light fast animal.

There is a dark bird called crow. There is a bright bird called gull. There is a slow light animal called crab. There is a light wet vapor called waves. There is a wet bright slow vapor called clouds. There is a wet dark slow vapor called fog. There is a bright solid called seashore. There is an expansive rock called cliff. There is a small rock called Boulder.

If a slow wet entity <emerges> a dry entity then the slow wet entity <drifts across> the dry entity.
If a vapor <billows up onto> an expansive solid then the vapor <lightly covers> the expansive solid.
If a fast animal <comes upon> a slow entity then the fast animal <scurries over> the slow entity.
If an expansive entity <bears down on> a small entity then the expansive entity <envelops> the small entity.
If a bird <flies into> an expansive entity then the bird <soars high above> the expansive entity.
If a bird <discovers> a small solid then the bird <settles upon> the small solid.
```
Notice that in the above example the first rule would need some editing. The dry entity must be removed from the value section of the rule cause in order for the rendering of the rule to make sense. This is because the first part of the sentence is used to render both the type and value of the cause section of the rule.
