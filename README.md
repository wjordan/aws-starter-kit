# cfn-starter-kit

This project contains a reference implementation (starter template and setup instructions) for an "infrastructure continuous delivery" architecture using GitHub, AWS CodePipeline and CloudFormation.

## Getting Started

1. [Fork this repo](fork).
2. Bootstrap the CloudFormation stack:
  a.   a. [![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json)
  b. Enter the forked repo's owner in the `GitHubOwner` field.
  c. Create a [New personal access token](https://github.com/settings/tokens/new) with `repo` and `admin:repo_hook` scopes, and enter the token in the `GitHubToken` field.
  d. Enter the name of an existing S3 bucket for storing pipeline artifacts in the `ArtifactBucket` field. ([Create a bucket](http://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) first if necessary.)
3. Verify the newly-created stack and pipeline.
  a. Check the [CloudFormation Console](https://console.aws.amazon.com/cloudformation) to ensure your stack reaches the `CREATE_COMPLETE` state successfully.
  b. Check the [CodePipeline Console](https://console.aws.amazon.com/codepipeline) to ensure the pipeline's `Source` and `Deploy` stages both completed successfully.
4. Update the CloudFormation stack:
  a. Modify `cfn-template.yml` in the Git repository and commit/push the change.
  b. For example, try renaming `Topic` to `NewTopic`.
5. Verify the stack update.
  a. Check the CodePipeline Console to ensure the pipeline processes the new commit in both stages.
  b. Check the CloudFormation Console to ensure your stack reaches the `UPDATE_COMPLETE` state successfully.
  c. Verify the created/updated resources. For example, check the [SNS Topics Console](https://console.aws.amazon.com/sns/v2/home#/topics) for the newly-created `NewTopic` resource.

That's it!

Note: The [CloudFormation Service Role](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-servicerole.html) (`CFNRole`) allows full permissions (`'*'`). For more restricted, fine-grained security, you should move the `CFNRole` and `PipelineRole` resources into a separate CloudFormation stack, reference them using [`Fn::ImportValue`](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-importvalue.html), and ensure that `CFNRole` [grants least privilege](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege).

## References

Talk from re:Invent 2016, "[Infrastructure Continuous Delivery Using AWS CloudFormation](https://www.youtube.com/watch?v=TDalsML3QqY)"
