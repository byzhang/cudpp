Design notes for cudppTune(), the auto-tuning interface for CUDPP Plans.

# Introduction #

Ideally we should only add a single new function to the public interface:
```
CUDPP_RESULT cudppTune(CUDPPHandle plan, CUDPPTuneConfig config);
```




In addition we add the CUDPPTuneConfig struct:

```
struct CUDPPTuneConfig
{
   CUDPPTuneOptions options; // or possibly a more flexible method
   float timeLimit;
   String tuneFilePath;
};
```

cudppTune() calls an internal tune function in the CUDPPPlan subclass indicated by the CUDPPHandle passed to it, which runs experiments as needed and changes parameters stored in the plan based on the results.

## Notes ##
  * Any CUDPPPlan subclass should have default settings that provide decent performance for common parameters so that any algorithm can be run without tuning.
  * The timeLimit field in CUDPPTuneConfig should have a reasonable default, and is to be used to limit the amount of time spent searching for an optimal tuning.
  * We need a mechanism for storing the tuning results between application runs.  See below.
  * We need to make sure it's easy to add tuning for new algorithms.  We should design a standard interface for querying tunable parameters and their valid ranges or values.

# Tuning Storage #

We have a few options for this:
  1. Global storage: a central file that stores tuning results for all applications and all algorithms.
  1. Per-application storage: a file stored in the current working directory when the application is run.  By making this configurable we can make this flexible for the user.
  1. No storage: this should be where we start since it will be easier to get things working.

## What we need to store ##

An algorithm tuning is basically an association of a set of parameters to an algorithm identifier.  If we want to be able to store tuning globally and look it up later, then we need to identify an algorithm using:
  * Algorithm name
  * Data size
  * Options

Parameters will vary from algorithm to algorithm, but they include things like CTA SIZE, elements per thread, and various algorithm-specific options.

## Storage Format ##
I (Mark) suspect we need something like [JSON](http://www.json.org/), which is designed as a lightweight data exchange file format.  We could use XML but it is more complex and heavy weight, and it's really designed as a document interchange format more than a data interchange format.

# Tuning Modularity #

We should endeavor to make it trivial to add tuning to a new algorithm. To do this, we should define an interface that CUDPPPlan subclasses must implement in order to be tunable.  This interface would include methods that allow the tuning system to query:

  * An ID for each tunable parameter
  * The type of the parameter: bool, uint, int, uint-list, int-list, float, etc.
  * The valid values for the parameter: obvious for bool, a delimited continuous range for int, uint, float, and a discrete list of valid values for int-list and uint-list.
  * The priority of the parameter.  So we can control the order in which parameter variations are tried. (Important due to the time limit.)

The interface should also provide methods that enable a plan to store its current configuration to a tuning file / database and also to find and load configuration from such a file/DB.

# Some general thoughts/questions(AAD) #
Where should the modeled data be held for a reduction there would only be a few parameters to save, and therefore putting it in the plan could be an option. However, as the method is generalized and extended to more complex input sets, the modeling data will increase quite a bit as well and it might make sense to store it within the tuning structure itself.
This would mean that each tuning structure would have to be similar to the cudppPlan concept, with an inherited class for flexible parameters... does it make sense to do it like this? Or just have each Plan carry its own separate tuning data.

The general organization would then be:
cudppTune() is called:
-it checks to see if this function has been tuned before and the associated values are stored somewhere (file)
-if not, it runs the tuner making sure to terminate and make a best guess if it runs past the timer limit.

cudppReduce() is called:
- it checks to see if the options from CUDPPTuneConfig are set
- if they are it grabs the modeling data and calculates the correct thread parameters
- if not it runs default

This the organization we want?
