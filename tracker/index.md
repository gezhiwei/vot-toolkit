Tracker module
==============

The tracker module contains tracker related functions. The toolkit is highly flexible in 
terms of integration of existing trackers that can be run as external programs 
that communicate with the toolkit using a special protocol. For more information
on the integration, please read the [integration document](integration.md) or look
at the examples in the `examples` directory.

Tracker descriptor
------------------

Each tracker is described using a tracker descriptor structure. The
structure contains the following fields:

-   **identifier** *(string)*: Each tracker has a unique identifier, 
       i.e. a string that is used to identify that particular tracker 
       within the evaluation system. Because of the simplicity there 
       are certain limitations to the type of characters that can be used in the identifier.
       See [valid_identifier](valid_identifier.m) function for more details.
-   **command** *(string)*: The tracker executable command with all
    command line arguments. Since
-   **directory** *(string)*: The directory where the results of the
    tracker are stored. This path is workspace dependent.
-   **label** *(string)*: Human friendly label of the tracker, less
    restricted than tracker identifier.
-   **metadata** *(structure)*: Additional metadata of the tracker.
-   **autogenerated** *(boolean)*: If the structure was autogenerated
    (the description file was not found).
-   **linkpath** *(structure)*: A cell array of paths that are used to
    set the system library path before executing the tracker. This way
    you can solve many linking issues.
-   **interpreter** *(string)*: Type of interpreter used, empty string
    by default.
-   **trax** *(boolean)*: True if the tracker executable supports TraX
    protocol.
-   **version** *(string, optional)*: Version of the tracker.
-   **family** *(string, optional)*: Family of the tracker.
-   **run** *(function)*: Function handle for the appropriate execution
    wrapper, either trax_wrapper or system_wrapper.

Most of the values in the descriptor are loaded from a tracker
definition file. The definition file is a Matlab/Octave script with the
name `tracker_<identifier>.m` that has to be visible to the interpreted
(located in path). The file should define the following variables that
are used by tracker_load to construct the descriptor structure:

-   **tracker_command** *(string)*: The executable command that is used to invoke the tracker program. Contains the full path to the executable and optional input arguments.
-   **tracker_label** *(string, optional)*: Human friendly label of the
    tracker. There are no restrictions to the format of the tracker label, but please try to keep it similar to the tracker identifier. If no value is given, the identifier is used instead.
-   **tracker_linkpath** *(cell, optional)*: An optional cell array of additional search-paths to be set before executing the tracker.
-   **tracker_interpreter** *(string, optional)*: The type of interpreter used or empty string. If you are using Matlab, enter `matlab` here.
-   **tracker_metadata** *(structure, optional)*: A structure of additional tracker information.
-   **tracker_trax** *(boolean, optional)*: An optional logical flag. If the variable exists and is true then the tracker is using the TraX protocol and will be executed as such.
-   **tracker_trax_parameters** *(structure, optional)*: Additional parameters that are passed to the tracker if the TraX protocol is used.

Module functions
----------------

### Creation

-   [tracker_create](tracker_create.m) - Create a new tracker configuration file
-   [tracker_load](tracker_load.m) - Create a new tracker descriptor structure
-   [tracker_list](tracker_list.m) - Create a set of tracker descriptor structures

### Execution

-   [tracker_evaluate](tracker_evaluate.m) - Evaluates a tracker on a given sequence for experiment
-   [prepare_trial_data](prepare_trial_data.m) - Prepares data for a trial run
-   [system_wrapper](system_wrapper.m) - Legacy approach to experiment execution
-   [trax_wrapper](trax_wrapper.m) - Tracker integration approach using TraX protocol

### Visualization

These functions are used to manipulate visualization information for trackers.

-   [set_trackers_visual_identity](set_trackers_visual_identity.m) - Generate visual identity information
-   [change_trackers_visual_identity](change_trackers_visual_identity.m) - Modify the visualization properties

### Utility

General utility functions for trackers.

-   [estimate_completion_time](estimate_completion_time.m) - Estimates completion time for a tracker
-   [calculate_results_fingerprint](calculate_results_fingerprint.m) - Calculate results hash
-   [find_tracker](find_tracker.m) - Find a tracker by its identifier
-   [is_deterministic](is_deterministic.m) - Test if a tracker is deterministic
-   [order_trackers](order_trackers.m) - Change the order of trackers
-   [valid_identifier](valid_identifier.m) - Verifies tracker identifier
-   [write_manifest](write_manifest.m) - Write a manifest file for the tracker
-   [benchmark_hardware](benchmark_hardware.m) - Perform a simple benchmark
-   [generate_matlab_command](generate_matlab_command.m) - Generate command line for Matlab trackers
-   [generate_python_command](generate_python_command.m) - Generate command line for Python trackers
-   [trax_test](trax_test.m) - Test support for TraX protocol
-   benchmark_native - A MEX function that performs several native benchmarks

