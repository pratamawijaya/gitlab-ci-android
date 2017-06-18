# gitlab-ci-android
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: pratamawijaya/gitlab-ci-android:latest

stages:
- check
- build
- deploy

before_script:
  - export GRADLE_USER_HOME=/cache/.gradle

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```


## How to create image from dockerfile and push it to dockerhub

- git clone url-dockerfile
- run `docker build -t image_name .`
- `docker image ls` for checking image
- `docker tage commitid pratamawijaya/gitlab-ci-android`
- `docker login`
- `docker push`