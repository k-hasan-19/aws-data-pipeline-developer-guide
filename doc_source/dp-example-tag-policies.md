# Example Policies for AWS Data Pipeline<a name="dp-example-tag-policies"></a>

The following examples demonstrate how to grant users full or restricted access to pipelines\.


+ [Example 1: Grant users read\-only access based on a tag](#ex1)
+ [Example 2: Grant users full access based on a tag](#ex2)
+ [Example 3: Grant the pipeline owner full access](#ex3)
+ [Example 4: Grant users access to the AWS Data Pipeline console](#example4-grant-users-access-to-console)

## Example 1: Grant users read\-only access based on a tag<a name="ex1"></a>

The following policy allows users to use the read\-only AWS Data Pipeline API actions, but only with pipelines that have the tag "environment=production"\. 

The ListPipelines API action does not support tag\-based authorization\.

```
{g
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "datapipeline:Describe*",
        "datapipeline:GetPipelineDefinition",
        "datapipeline:ValidatePipelineDefinition",
        "datapipeline:QueryObjects"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringEquals": {
          "datapipeline:Tag/environment": "production"
        }
      }
    }
  ]
}
```

## Example 2: Grant users full access based on a tag<a name="ex2"></a>

The following policy allows users to use all AWS Data Pipeline API actions, with the exception of ListPipelines, but only with pipelines that have the tag "environment=test"\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "datapipeline:*"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringEquals": {
          "datapipeline:Tag/environment": "test"
        }
      }
    }
  ]
}
```

## Example 3: Grant the pipeline owner full access<a name="ex3"></a>

The following policy allows users to use all the AWS Data Pipeline API actions, but only with their own pipelines\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "datapipeline:*"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringEquals": {
          "datapipeline:PipelineCreator": "${aws:userid}"
        }
      }
    }
  ]
}
```

## Example 4: Grant users access to the AWS Data Pipeline console<a name="example4-grant-users-access-to-console"></a>

The following policy allows users to create and manage a pipeline using the AWS Data Pipeline console\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:*",
        "datapipeline:*",
        "dynamodb:DescribeTable",
        "elasticmapreduce:AddJobFlowSteps",
        "elasticmapreduce:ListInstance*",
        "iam:AddRoleToInstanceProfile",
        "iam:CreateInstanceProfile",
        "iam:GetInstanceProfile",
        "iam:GetRole",
        "iam:ListInstanceProfiles",
        "iam:ListInstanceProfilesForRole",
        "iam:ListRoles",
        "iam:PassRole",
        "rds:DescribeDBInstances",
        "rds:DescribeDBSecurityGroups",
        "redshift:DescribeClusters",
        "redshift:DescribeClusterSecurityGroups", 
        "s3:List*",
        "sns:ListTopics"
      ],
      "Resource": "*"
    }
  ]
}
```