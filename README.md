# Directed Graphs

Directed graphs comprised of directed acyclic graphs together with cycles.

### Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Building](#building)
- [Contact](#contact)

## Introduction

The reason for not simply implementing a directed graph trivially is to keep track of cycles and recover them quickly. Given the name of any vertex, the implementation will report whether or not it is part of a cycle. If it is, you can retrieve a cycle of which it is part, but bear in mind that a vertex may be the part of more than one cycle, any one of which can be returned.

## Installation

With [npm](https://www.npmjs.com/):

    npm install occam-directed-graph

You can also clone the repository with [Git](https://git-scm.com/)...

    https://github.com/jecs-imperial/occam-directed-graph.git

...and then install the necessary modules with npm from within the project's root directory:

    npm install

## Usage
    
An empty directed graph can be created by calling the `fromNothing()` factory method, after which vertices and edges can be added incrementally:

```js
const directedGraphs = require('occam-directed-graphs');

const { DirectedGraph, Edge } = directedGraphs;

const directedGraph = DirectedGraph.fromNothing(),
      vertexName = 'i',
      sourceVertexName = 'j',
      targetVertexName = 'k';

directedGraph.addVertexByName(vertexName);

directedGraph.addEdgeByVertexNames(sourceVertexName, targetVertexName);
```

Note that there is no need to added vertices explicitly, they will be added whenever necessary when edges that reference them are added.

Alternatively, a directed graph can be constructed with the `fromVertexLiterals()` factory method as follows:

```js
const directedGraphs = require('occam-directed-graphs');

const { DirectedGraph } = directedGraphs;

const graph = Graph.fromVertexLiterals([

  ['a', ['b']],
  ['b', ['c']],
  ['d', ['c']],
  ['e', []],
  ['f', ['g']],
  ['h', ['g']]

]);
```

Note that the array of names that is the second element of each literal gives the *ancestors* of the vertex and not its descendants.

You can also remove vertices and edges from the graph. Removing a vertex may of course result in removing edges. When you remove an edge, you can additionally specify that the any stranded vertices that result are also removed:

```js
const vertexName = 'i',
      sourceVertexName = 'j',
      targetVertexName = 'k',
      removeStrandedVertices = true;

directedGraph.removeVertexByName(vertexName);

directedGraph.removeEdgeByVertexNames(sourceVertexName, targetVertexName, removeStrandedVertices);
```

The default is to leave stranded vertices in place.

Finally, you can detect and recover cycles thus:

```js
const vertexName = 'i',
      cyclePresent = directedGraph.isCyclePresentByVertexName(vertexName);

if (cyclePresent) {
  const cycle = directedGraph.getFirstCycleByVertexName(vertexName),
        cycleVertexNames = cycle.getVertexNames();

  ...
}
```
As already pointed out in the introduction, if a vertex is part of more than one cycle, any of of them can be given.

## Building

Automation is done with [npm scripts](https://docs.npmjs.com/misc/scripts), have a look at the `package.json` file. The pertinent commands are:

    npm run build-debug
    npm run watch-debug

## Contact

* james.smith@openmathematics.org
* http://djalbat.com
