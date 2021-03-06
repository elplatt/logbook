# repsci
Reproducible computational science

Installing.

    pip install repsci

Import the logging library.

    import repsci

Create an experiment. A unique directory will be created with the experiment
name, a timestamp, and the current git hash.

    exp_name = "hello_world"
    exp = repsci.Experiment(exp_name)

Get the logger and write a log message.

    log = exp.get_logger()
    log.debug("Hello, World!")

Create an output file in the unique output directory.

    filename = exp.get_filename('output.csv')
    with open(filename, "wb") as f:
        f.write("Hello, World\n")

The state of python's random number generator is stored in `random_state.bin`
in pickle format. This state can be used to reproduce the output of randomized
scripts.
        
The Experiment constructor also has some optional parameters:
* `note`: a string of notes to store in a `notes.txt` file in the output directory.
* `config`: a configparser object, which will exported to the output directory.
* `output_dir`: the subdirectory of the current directory to place experiment directories in.
* `suffix`: a string to append to the end of the trial's directory.

Create an experiment from a previous experiment's unique directory.

    exp_name = "hello_world"
    timestamp = "2020-09-09 152600"
    exp = repsci.Experiment(exp_name, reproduce=timestamp)
    
Get the config from the prevous experiment.

    config = exp.get_config()
