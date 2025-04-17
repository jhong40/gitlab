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
```
```
deploy:
  stage: deploy
  script:
    - echo "Deploying branch: $CI_COMMIT_REF_NAME"
    - ./deploy.sh --env=$CI_COMMIT_REF_NAME
```
