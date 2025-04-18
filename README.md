# gitlab
```
.base-job:
  script:
    - echo "Common step 1"
    - |
      if [ "$CUSTOM" == "true" ]; then
        echo "Custom step 2"
      else
        echo "Default step 2"
      fi

.job-uses-custom:
  extends: .base-job
  variables:
    CUSTOM: "true"
-------------------
deploy:
  stage: deploy
  script:
    - echo "Deploying branch: $CI_COMMIT_REF_NAME"
    - ./deploy.sh --env=$CI_COMMIT_REF_NAME


-------------------
.vars:
  variables:
    URL: "http://my-url.internal"
    IMPORTANT_VAR: "the details"

test-vars-1:
  variables: !reference [.vars, variables]
  script:
    - printenv

test-vars-2:
  variables:
    MY_VAR: !reference [.vars, variables, IMPORTANT_VAR]
  script:
    - printenv
```
