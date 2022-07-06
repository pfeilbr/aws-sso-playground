# aws-sso-playground

learn [AWS SSO](https://docs.aws.amazon.com/singlesignon/index.html)

---

## SSO Access Token

The `aws sso` CLI commands require the `--access-token` parameter.  First login via sso (e.g. `aws sso login --profile root-AWSAdministratorAccess`), then run the following to get.

```sh
# get cached aws sso accessToken
function aws-access-token() { cat $(ls -1d ~/.aws/sso/cache/* | grep -v botocore) |  jq -r "{accessToken} | .[]" }
```

---

## Demo

list account assignments ([AWS::SSO::Assignment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sso-assignment.html))

```sh
aws sso-admin list-account-assignments \
    --instance-arn 'arn:aws:sso:::instance/ssoins-72234101455cbc87' \
    --account-id '529276214230' \
    --permission-set-arn 'arn:aws:sso:::permissionSet/ssoins-72234101455cbc87/ps-51eacb02632f0b26'

```

```json
{
    "AccountAssignments": [
        {
            "AccountId": "529276214230",
            "PermissionSetArn": "arn:aws:sso:::permissionSet/ssoins-72234101455cbc87/ps-51eacb02632f0b26",
            "PrincipalType": "USER",
            "PrincipalId": "906770ec60-e34082a0-033a-4dd2-90cb-9107804545e9"
        },
        {
            "AccountId": "529276214230",
            "PermissionSetArn": "arn:aws:sso:::permissionSet/ssoins-72234101455cbc87/ps-51eacb02632f0b26",
            "PrincipalType": "USER",
            "PrincipalId": "906770ec60-9d6f0b65-701c-4650-b95c-7dab0f6046d7"
        }
    ]
}
```

## Resources

- [AWS Single Sign-On Documentation](https://docs.aws.amazon.com/singlesignon/index.html)
- [aws sso-admin](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sso-admin/index.html) - cli
- [benkehoe/aws-sso-util](https://github.com/benkehoe/aws-sso-util)
- [AWS::SSO::PermissionSet](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sso-permissionset.html)
- [AWS::SSO::Assignment](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sso-assignment.html)
- [How can I get temporary credentials for an AWS Single Sign-On user using the AWS CLI?](https://aws.amazon.com/premiumsupport/knowledge-center/sso-temporary-credentials/)