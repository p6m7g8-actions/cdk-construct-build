# p6m7g8-actions/cdk-construct-build

- [p6m7g8-actions/cdk-construct-build](#p6m7g8-actionscdk-construct-build)
  - [Usage](#usage)

## Usage

```yml
      - name: CDK Construct Build
        uses: p6m7g8-actions/p6-cdk-construct-build@main
        with:
          aws_region: ${{ secrets.CDK_DEPLOY_REGION }}
          aws_role: ${{ secrets.AWS_ROLE }}
          aws_session_name: ${{ secrets.AWS_SESSION_NAME }}
          cdk_deploy_account: ${{ secrets.CDK_DEPLOY_ACCOUNT }}
          cdk_deploy_region: ${{ secrets.CDK_DEPLOY_REGION }}
```

## When AWS credentials are required

The AWS inputs are optional, and the OIDC role-assumption step is skipped when
`aws_role` is empty. A construct build that only runs `jsii` codegen needs no AWS
at all, and previously failed at the credentials step for no reason.

The consequence is worth knowing: an unset or misnamed `AWS_ROLE` secret renders
as an empty string, so the step is skipped rather than failing loudly. If your
`ci:gha` performs CDK context lookups such as `Vpc.fromLookup` or an SSM image
lookup, pass `aws_role` and grant `id-token: write`, or those lookups will fail
later with an opaque AWS error instead of a clear one here.
