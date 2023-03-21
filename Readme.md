# B-MATH-200-107transfer - Unit Tests

Any tests for 107transfer Epitech Project

These tests are written in YAML and runned with [BinaryTester](https://github.com/Epitests-unofficial/BinaryTester.git)

#### Tests Running

* Clone this repo
* Install [BinaryTester](https://github.com/Epitests-unofficial/BinaryTester.git)
* Go to your project directory and copy test.yaml in your repo
* run `binaryTester test.yaml`

#### Jenkins Pipeline

You can setup a Jenkins pipeline with these tests by this way :

* Download and install [Abricot Norminette](https://https://github.com/Just1truc/Abricot-Norminette) Epitech Coding Style in your Jenkins installation
* Just download the Jenkinsfile (in this repo) and move it at the root of your repo.
* In Jenkins create a new Pipeline and setup with `Pipeline script from SCM` with your personnal repo
* You can set up a Poll SCM settings in build trigger in order to run tests at each update
* Run a first test
