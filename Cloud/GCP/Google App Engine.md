# Abstract
- [[Elastic Beanstalk]]에 대응하는 서비스
# Content
## App Engine에서 사용하는 [[Google Cloud Storage Bucket]]
- [링크 참조](https://stackoverflow.com/questions/60803473/google-cloud-app-engine-default-storage-buckets)
> When you create an app, App Engine creates a default bucket that provides the first 5GB of storage for free. The default bucket also includes a free quota for Cloud Storage I/O operations. See Pricing, quotas, and limits for details. You will be charged for storage over the 5GB limit.
  > 
  > The name of the default bucket is in the following format:
  > 
  > **project-id.appspot.com**
  > 
  > App Engine also creates a bucket that it uses for temporary storage when it deploys new versions of your app. This bucket, named **staging.project-id.appspot.com**, is for use by App Engine only. Apps can't interact with this bucket.
  
  **eu.artifacts.yyy.appspot.com** is your [container registry](https://cloud.google.com/container-registry/docs/access-control) bucket
  
  > Your Container Registry bucket URL will be listed as gs://artifacts.[PROJECT-ID].appspot.com or gs://[STORAGE-REGION].artifacts.[PROJECT-ID].appspot.com, where:
  > 
  > [PROJECT-ID] is your Google Cloud Console project ID. Domain-scoped projects will have the domain name as part of the project ID. [STORAGE-REGION] is the location of the storage bucket: us for registries in the host us.gcr.io **eu for registries in the host eu.gcr.io** asia for registries in the host asia.gcr.io
# Reference
- [Strapi v3 - Google App Engine](https://docs-v3.strapi.io/developer-docs/latest/setup-deployment-guides/deployment/hosting-guides/google-app-engine.html)