
# CloudFormation


## CloudFormation Best Practices
* Use Infrastructure as Code to manage as much infrastructure as you can. Avoid manual configurations whenever possible.
* Treat your templates as code: use version control!
* Modularize templates by separating your resources in multiple files. Avoid large templates, they become unmanageable! When doing the split, try to think in the lifecycle and team ownership of your resources.
* Use parameter files to reuse templates when deploying the same resources to different environments.
* Do not embed credentials in your templates. You can always pass them securely as parameters or leverage more advanced AWS features to handle secrets.

## Intrinsic Functions

!Ref  
Returns a parameter value or the physical ID of a resource. We met this function while reviewing parameters:

    !Ref EnvironmentName

!GetAtt  
Returns a specific property from a resource. For example, to get the CIDR block of a VPC:

    !GetAtt Vpc.CidrBlock

!Sub  
Returns an interpolated string resulting from replacing placeholders in an input string with static or dynamic values. For example, you can create a new string using the EnvironmentName variable:

    !Sub My environment name is ${EnvironmentName}

