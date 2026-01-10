# p6m7g8-actions/cdk-construct-build

- [p6m7g8-actions/cdk-construct-build](#p6m7g8-actionscdk-construct-build)
  - [Usage](#usage)

## Usage

```yml
      - name: CDK Construct Build
        uses: p6m7g8-actions/cdk-construct-build@main
        with:
          aws_region: ${{ secrets.CDK_DEPLOY_REGION }}
          aws_role: ${{ secrets.AWS_ROLE }}
          aws_session_name: ${{ secrets.AWS_SESSION_NAME }}
          cdk_deploy_account: ${{ secrets.CDK_DEPLOY_ACCOUNT }}
          cdk_deploy_region: ${{ secrets.CDK_DEPLOY_REGION }}
```
