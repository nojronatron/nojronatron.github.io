# Java Naming Conventions

Oracle has a reference that fully describes Java naming conventions.  
Here I will rapidly summarize many/most of them as part of my learning process.  

## Reference

For the full meal deal, see [Oracle JavaSE Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html)  

Let it also be known that most of these examples are pulled DIRECTLY from *[Oracle JavaSE Documentation]* (see above).  

## Convensions

ID Type => Example

Packages => All lowercase => `'com.sun.eng', 'com.apple.quicktime.v2', 'edu.cmu.us.bovik.cheese'`  
Classes => Mixed-case Nouns => `'class Raster', 'class ImageSprite'`  
Interfaces => Capitalized => `'interface RasterDelegate', 'interface Storing'`  
Methods => Mixed-case Verbs => `'run()', 'runFast()', 'getBackground()'`  
Variables => camelCase mnemonic words => `'int integer;', 'char charCharacter', 'float itemWidth'`  
Constants => Underscore-separated uppercased words => `'static final int MIN_WIDTH = 4;', static final int MAX_WIDTH = 999;', static final int GET_THE_CPU = 1;'`  

## Footer

Return to [Parent Readme.md](../README.html)  
