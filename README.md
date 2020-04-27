# ML project workflow

## Project

1. `bin` - bash files for running pipelines, place all `.sh` files here
1. `common` - data preprocessing scripts, utils, everything like
    ```
    python common/scripts/{some-script}.py
    # or
    from common import utils
   ```
   typically, it our project/library core
1. `docker` - project Docker files for pure reproducibility
1. `presets` - datasets, notebooks, etc - all you don't need to push to git, use
    - `presets/data` for datasets
    - `presents/notebooks` for notebooks
    - `presets/serving` for serving artefacts
1. `requirements` - different project python requirements for docker, tests, CI, etc
1. `serving` - microservices, etc - production with [Reaction](https://github.com/catalyst-team/reaction)
1. `training` - model, experiment, etc - research with [Alchemy](https://github.com/catalyst-team/alchemy) & [Catalyst](https://github.com/catalyst-team/catalyst), use
    - `training/configs` - for all configs, just all `.yml` files


## Workflow
tip: you can save all answers to `presets/_faq.md`.


#### Before ML (miniFAQ)

1. What problem are you trying to solve?
1. How do you think it can be solved? What is your hypothesis?
1. What is the value of the hypothesis you are testing?
1. What are the main metrics? How to measure them?
1. How can metrics prove that hypothesis works?
1. Is it possible to check it without ML? How?
1. How will your solution be integrated into the current system?
1. What can go wrong? What kind of corner cases can occur?

#### ML (plan)

1. Perform data exploratory analysis, check that the data and labeling are correct.
1. Plot main statistics, find outliers and recheck them again.
1. Do data preprocessing, get clean data from raw one.
1. Split data into train/valid/test parts and fix this data split for future experiments.
1. Run `adversarial split` on your train/valid/test parts to check split correctness. 
1. Overfit your model on one batch from train part to ensure, that pipeline work correctly.
1. Use train/valid parts for model training (log all your experiments) and valid part for model final postrocessing.
1. Track metrics for all experiments (use tables for this). Do not forget to write tests for used metrics.


#### After ML (todo)

1. Write down all experiments, check their performance on test part, select best one.
1. Trace the model :)


## Extra

To keep your code simple and readable, you can use [catalyst-codestyle](https://github.com/catalyst-team/codestyle)
```bash
# install
pip install -U catalyst-codestyle
# and run
catalyst-make-codestyle && catalyst-check-codestyle
```
