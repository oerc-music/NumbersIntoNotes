Generate MEI and MELD files
===========================

This details how to automate generation of MEI and MELD files with Javascript.

When generation is occurring it will highlight the areas it is selecting on screen. 
A window opens to capture the post responses.

Quick Example
-------------

For a quick example open the console and run the function:

	agDoSample()
	
This will generate 81 different values, but grouped by length, pitch and function.

Export settings
---------------

An "export setting" consists of the following changeable values :

	{
		number: 3,              // number of fragments to generate with these values
		length: 8,              // the length of a fragment
		modulus: 35,            // number to reduce to
		func: doFibonacci,      // function used to generate 
		funcParams: [0,1,1],    // parameters for function
		pitch: 2,               // pitch
		octave: 2,              // pitch
		scale: [2,2,1,2,2,2,1], // pitch
	}

You can call the function agGetExport() (incidetnally, all the function names begin with "ag") 
to generate an export object, it will use the above defined defaults.
You can also generate a randomised version of this by passing in true

	agGetExport(true)
	
it uses the following domains:

    {
        number: rand(3, 8),
        length: rand(5, 10),
        modulus: rand(17, 35) ,
        func: funcs[rand(0,funcs.length-1)],
        funcParams: null, /* not radomisation here, default values in each function used */
        pitch: rand(0, 11),
        octave: rand(0, 7),
        scale: scales[rand(0,scales.length-1)],
    }

the function can be one of these (you can pass non-default parameters via funcParams):

	var funcs = [
		doFibonacci,                // parameters: n0, n1, k
		doPowers,                  // parameters: b
	
		doPrimes,                   // parameters: n
		doPi,                       // parameters: n
		doPhi,                      // parameters: n
		doRandom,                   // parameters: n
		doDiceWalk,                 // parameters: n
	
		doTribonacci,               // parameters: n0, n1, n2
		doTriangle,                 // parameters:
		doFactorial,                // parameters:
		doSin,                      // parameters: a, r
		doBernoullinumerators,      // parameters: n
		doBernoullidenominators     // parameters: n
	];

the scale can be one of:

	var scales = [
		[2,2,1,2,2,2,1],    // Major
		[2,1,2,2,1,2,2],    // Natural minor
		[2,1,2,2,1,3,1],    // Harmonic minor
		[2,2,1,2,1,3,1],    // Harmonic major
		[2,2,3,2,3],        // Pentatonic
		[2],                // Whole Tone
		[1]                 // Chromatic
	];

To use the export settings, create an array and 
pass it into `agStart`, e.g.:

	var settingsList = [];
	for( var i=0; i < 10; i++ ) {
		settingsList.push( agGetExport(true); );
	}
	agStart(settingsList);

If you'd like to generate but e.g. use a single function, just adjust that particular value:

		var settingsList = [];
		for( var i=0; i < sets; i++ ) {
			var setting = agGetExport(true);
			setting.function = doFibanacci;
			settingsList.push( setting );
		}
		agStart(settingsList);

There are also few helper functions to help generate sets.

 - `agDoSample()` will generate a nice selection of settings
 - `agDoRandomSets( sets, number )` will generate a random set, then produce 
several with the same settings (but random position)
 - `agDoDifferentLengthsSet()` will generate the same values all but length
 - `agDoAllFuncsSet` will generate the same values for each function available.

