# finmath lib cuda extensions
- - - -
**Enabling finmath lib with cuda via jcuda.**
- - - -
The finmath lib cuda extension provide an implementation of the finmath lib interfaces `RandomVariableInterface` and `BrownianMotionInterface`` compatible with finmath lib 2.4.3 or later.

Since objects of type `BrownianMotionInterface` are taking the role of a factory for objects of type `RandomVariableInterface`, injecting the `BrownianMotionCuda` will result in most finmath-lib models performing their calculations on the GPU - seamlessly.

## Example
Create a vector of floats on the device
```
RandomVariableInterface randomVariable = new RandomVariableCuda(new float[] {-4.0f, -2.0f, 0.0f, 2.0f, 4.0f} );
```
perform some calculations (still on the gpu device)
```
randomVariable = randomVariable.add(4.0);
randomVariable = randomVariable.div(2.0);
```
perform a reduction on the device
```
double average = randomVariable.getAverage();
```
or get the result vector
```
double[] result = randomVariable.getRealizations();
```
(note: the result is always double, since different implementation may support float or double on the device).

## Installation
Of course, you should have NVidia Cuda installed.

In addition, the finmath-lib-cuda-extensions requires jcuda. To install jcuda you should try the  "mavenized" version of jcuda.  To obtain and build the mavenized version of jcuda:
```
git clone https://github.com/MysterionRise/mavenized-jcuda.git
cd mavenized-jcuda
mvn clean package
cd ..
```

To obtain and build the finmath-lib-cuda-extensions then do
```
git clone https://github.com/cfries/finmath-lib-cuda-extensions.git
cd finmath-lib-cuda-extensions
mvn clean package
```
If everything goes well, you will see unit test  run. Note that some of the tests mail fail if the device (GPU) has not enough memory. 

## References
* [finmath lib Project documentation](http://finmath.net/finmath-lib/)
provides the documentation of the library api.
* [finmath lib API documentation](http://finmath.net/finmath-lib/apidocs/)
provides the documentation of the library api.
* [finmath.net special topics](http://www.finmath.net/topics)
cover some selected topics with demo spreadsheets and uml diagrams.
Some topics come with additional documentations (technical papers).

## License
The code of "finmath lib", "finmath experiments" and "finmath lib cuda extensions" (packages
`net.finmath.*`) are distributed under the [Apache License version
2.0](http://www.apache.org/licenses/LICENSE-2.0.html), unless otherwise explicitly stated.
