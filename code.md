### Git Store password
git config --global credential.helper store
git config --global user.email "jingxi@me.com"
git config --global user.name "jingxi"


### Mindmap Note

```mermaid
graph LR
y(core)-->A(industry)-->B2(MFG)
B2-->C1(GoCode)
B2-->C2(PCode)
```

### CI/CD
```

# This file is a template, and might need editing before it works on your project.
# This is a sample GitLab CI/CD configuration file that should run without any modifications.
# It demonstrates a basic 3 stage CI/CD pipeline. Instead of real tests or scripts,
# it uses echo commands to simulate the pipeline execution.
#
# A pipeline is composed of independent jobs that run scripts, grouped into stages.
# Stages run in sequential order, but jobs within stages run in parallel.
#
# For more information, see: https://docs.gitlab.com/ee/ci/yaml/index.html#stages
#
# You can copy and paste this template into a new `.gitlab-ci.yml` file.
# You should not add this template to an existing `.gitlab-ci.yml` file by using the `include:` keyword.
#
# To contribute improvements to CI/CD templates, please follow the Development guide at:
# https://docs.gitlab.com/ee/development/cicd/templates.html
# This specific template is located at:
# https://gitlab.com/gitlab-org/gitlab/-/blob/master/lib/gitlab/ci/templates/Getting-Started.gitlab-ci.yml
stages:          # List of stages for jobs, and their order of execution
  - build
  - test
  - deploy
# image: mcr.microsoft.com/dotnet/sdk:6.0.406-jammy-amd64
build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    - echo "Compiling the code..."
    - ls
    - dotnet restore
    - echo "Compile complete."
unit-test-job:   # This job runs in the test stage.
  stage: test    # It only starts when the job in the build stage completes successfully.
  script:
    - echo "Running unit tests... This will take about 60 seconds."
    - echo "sleep 60"
    #- dotnet test --no-build -c Release   -l  "trx;LogFileName=../../testRes.trx"
    - dotnet test   -l  "trx;LogFileName=../../testRes.trx"
  
    #- echo "Code coverage is 90%"
  after_script:
     - /root/.dotnet/tools/trx2junit testRes.trx
  artifacts:
    when: always
    paths: ['testRes.xml']
    expose_as: 'testing report'
    reports:
      junit: testRes.xml

 
deploy-job:      # This job runs in the deploy stage.
  stage: deploy  # It only runs when *both* jobs in the test stage complete successfully.
  script:
    - echo "Deploying application..."
    - echo "Application successfully deployed."

```
