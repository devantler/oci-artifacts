# LocalAI

A free OpenAI drop-in alternative for AI/ML models. It requires no GPU or internet connection to run, and can thus be used as a AI service for Kubernetes applications.

## Post-build variables

| Variable                         | Description                                        | Default       | Required |
| -------------------------------- | -------------------------------------------------- | ------------- | -------- |
| local_ai_image_tag               | The tag of the LocalAI image                       | latest        | ✕        |
| local_ai_ingress_enabled         | Enable ingress for LocalAI                         | true          | ✕        |
| local_ai_persistence_access_mode | The access mode for the LocalAI persistence volume | ReadWriteMany | ✕        |
