GeneticSharp
===========
[![Build Status](https://travis-ci.org/giacomelli/GeneticSharp.png?branch=master)](https://travis-ci.org/giacomelli/GeneticSharp)

GeneticSharp is a fast, extensible, multi-platform and multithreading .NET Genetic Algorithm library that simplifies the development of applications using Genetic Algorithms (GAs).

Can be used in ASP .NET MVC, Web Forms, Windows Forms, GTK# and Unity3D applications.

--------

Features
===
 - Chromosomes
   - Add your own chromosome representation implementing [IChromosome](src/GeneticSharp.Domain/Chromosomes/IChromosome.cs) interface or extending [ChromosomeBase](src/GeneticSharp.Domain/Chromosomes/ChromosomeBase.cs)   
 - [Fitness](src/GeneticSharp.Domain/Fitnesses)
   - Add your own fitness evaluation, implementing [IFitness](src/GeneticSharp.Domain/Fitnesses/IFitness.cs) interface.
 - [Populations](src/GeneticSharp.Domain/Populations)
   - [Generation](src/GeneticSharp.Domain/Populations/Generation.cs)
   - [Generation strategy](src/GeneticSharp.Domain/Populations/IGenerationStrategy.cs)
     - [Performance strategy](src/GeneticSharp.Domain/Populations/PerformanceGenerationStrategy.cs)
     - [Tracking strategy](src/GeneticSharp.Domain/Populations/TrackingGenerationStrategy.cs)  
 - [Selections](src/GeneticSharp.Domain/Selections)
   - [Elite](src/GeneticSharp.Domain/Selections/EliteSelection.cs) (also know as Truncate or Truncation)
   - [Roulette Wheel](src/GeneticSharp.Domain/Selections/RouletteWheelSelection.cs)
   - [Stochastic Universal Sampling](src/GeneticSharp.Domain/Selections/StochasticUniversalSamplingSelection.cs)
   - [Tournament](src/GeneticSharp.Domain/Selections/TournamentSelection.cs)  
   - Others selections can be added implementing [ISelection](src/GeneticSharp.Domain/Selections/ISelection.cs) interface or extending [SelectionBase](src/GeneticSharp.Domain/Selections/SelectionBase.cs). 
 - [Crossovers](src/GeneticSharp.Domain/Crossovers)
   - [Cut and Splice](src/GeneticSharp.Domain/Crossovers/CutAndSpliceCrossover.cs) 
   - [Cycle (CX)](src/GeneticSharp.Domain/Crossovers/CycleCrossover.cs)   
   - [One-Point](src/GeneticSharp.Domain/Crossovers/OnePointCrossover.cs)
   - [Ordered OX1](src/GeneticSharp.Domain/Crossovers/OrderedCrossover.cs)
   - [Partially Mapped (PMX)](src/GeneticSharp.Domain/Crossovers/PartiallyMappedCrossover.cs)
   - [Three parent](src/GeneticSharp.Domain/Crossovers/ThreeParentCrossover.cs)
   - [Two-Point](src/GeneticSharp.Domain/Crossovers/TwoPointCrossover.cs)
   - [Uniform](src/GeneticSharp.Domain/Crossovers/UniformCrossover.cs)
   - Others crossovers can be added implementing [ICrossover](src/GeneticSharp.Domain/Crossovers/ICrossover.cs) interface or extending [CrossoverBase](src/GeneticSharp.Domain/Crossovers/CrossoverBase.cs).   
 - [Mutations](src/GeneticSharp.Domain/Mutations)
   - [Reverse Sequence (RSM)](src/GeneticSharp.Domain/Mutations/ReverseSequenceMutation.cs)
   - [Twors](src/GeneticSharp.Domain/Mutations/TworsMutation.cs)
   - [Uniform](src/GeneticSharp.Domain/Mutations/UniformMutation.cs)
   - Others mutations can be added implementing [IMutation](src/GeneticSharp.Domain/Mutations/IMutation.cs) interface or extending [MutationBase](src/GeneticSharp.Domain/Mutations/MutationBase.cs).
 - [Reinsertions](src/GeneticSharp.Domain/Reinsertions)
   - [Elitist](src/GeneticSharp.Domain/Reinsertions/ElitistReinsertion.cs)
   - [Fitness Based](src/GeneticSharp.Domain/Reinsertions/FitnessBasedReinsertion.cs)
   - [Pure](src/GeneticSharp.Domain/Reinsertions/PureReinsertion.cs)
   - [Uniform](src/GeneticSharp.Domain/Reinsertions/UniformReinsertion.cs)
 - [Terminations](src/GeneticSharp.Domain/Terminations)
   - [Generation number](src/GeneticSharp.Domain/Terminations/GenerationNu)
   - [Time evolving](src/GeneticSharp.Domain/Terminations/TimeEvolvingTermination.cs)
   - [Fitness stagnation](src/GeneticSharp.Domain/Terminations/FitnessStagnationTermination.cs)
   - [Fitness threshold](src/GeneticSharp.Domain/Terminations/FitnessThresholdTermination.cs)
   - [And](src/GeneticSharp.Domain/Terminations/AndTermination.cs) e [Or](src/GeneticSharp.Domain/Terminations/OrTermination.cs) (allows combine others terminations)
 - [Randomizations](src/GeneticSharp.Domain/Randomizations)
   - [Basic randomization](src/GeneticSharp.Domain/Randomizations/BasicRandomization.cs) (using System.Random)
   - [Fast random](src/GeneticSharp.Domain/Randomizations/FastRandomRandomization.cs)   
   - If you need a special kind of randomization for your GA, just implement the [IRandomization](src/GeneticSharp.Domain/Randomizations/IRandomization.cs) interface.
 - [Runner app (GTK#)](src/GeneticSharp.Runner.GtkApp) showing the library solving TSP (Travelling Salesman Problem).
 
 	![](docs/screenshots/GtkApp.Samples.TSP.Win.png)
 - Mono support
 
 	![](docs/screenshots/XamarinStudio.png) 
 	![](docs/screenshots/VisualStudio.png) 
 - Fully tested on Windows and MacOSX
 
 	![](docs/screenshots/GtkApp.Samples.TSP.Mac.png)
 - 100% Unit Tests coveraged 
 
	![](docs/screenshots/UnitTests.png)
 - 100% code [documentation](src/Help/Documentation.chm)
 - FxCop validated
 - Good (and good used) design patterns  

--------


Usage
===

Creating your own fitness evaluation 
---
```csharp

public class YourIFitnessImplementation : IFitness
{  
	public double Evaluate (IChromosome chromosome)
	{
		// Evaluate the fitness of chromosome.
	}
}

```

Creating your own chromosome 
---
```csharp

public class YourIChrosomeImplementation : ChromosomeBase
{
	public override Gene GenerateGene (int geneIndex)
	{
		// Generate a gene base on your chromosome representation.
	}

	public override IChromosome CreateNew ()
	{
		return new YourIChrosomeImplementation();
	}
}

```

Running your GA 
---
```csharp

var selection = new EliteSelection();
var crossover = new OrderedCrossover();
var mutation = new ReverseSequenceMutation();
var fitness = new YourIFitnessImplementation();
var chromosome = new YourIChrosomeImplementation(); // please, don't use names like that ;)
var population = new Population (50, 70, chromosome);

var ga = new GeneticAlgorithm(population, fitness, selection, crossover, mutation);

ga.Start();

```

--------

Roadmap
--------
 - Improve Runner.GtkApp
   - Add new problems/classic samples
      - Checkers 
	  - Time series   
 - Create and publish NuGet package
 - Create the wiki
 - Add new selections   
   - Reward-based
 - Add new crossovers   
   - Order-based (OX2)
   - Position-based (POS)
   - Voting recombination
   - Alternating-position (AP)
   - Sequential Constructive (SCX)    
   - Shuffle crossover
   - Precedence Preservative Crossover (PPX)
 - Add new mutations
   - Non-Uniform
   - Flip Bit
   - Boundary
   - Gaussian 
 - Add new terminations
   - Fitness convergence 
   - Population convergence
   - Chromosome convergence   
 - Unity3d game sample (WIP)
 - MonoTouch Runner app (sample)
 - Parallel populations (islands) 
 
--------

How to improve it?
======

Create a fork of [GeneticSharp](https://github.com/giacomelli/GeneticSharp/fork). 

Did you change it? [Submit a pull request](https://github.com/giacomelli/GeneticSharp/pull/new/master).


License
======

Licensed under the The MIT License (MIT).
In others words, you can use this library for developement any kind of software: open source, commercial, proprietary and alien.


Change Log
======
0.5.0 First version.
