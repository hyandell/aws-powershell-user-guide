# Specifying AWS Regions<a name="pstools-installing-specifying-region"></a>

There are two ways to specify the AWS Region to use when running AWS Tools for PowerShell commands:
+ Use the `-Region` common parameter on individual commands\.
+ Use the `Set-DefaultAWSRegion` command to set a default Region for all commands\.

Many AWS cmdlets fail if the Tools for Windows PowerShell can't figure out what Region to use\. Exceptions include cmdlets for [Amazon S3](pstools-s3.md), Amazon SES, and [IAM and Tools for PowerShell](pstools-iam.md), which automatically default to a global endpoint\.

 **To specify the region for a single AWS command** 

Add the `-Region` parameter to your command, such as the following\.

```
PS > Get-EC2Image -Region us-west-2
```

 **To set a default region for all AWS CLI commands in the current session** 

From the PowerShell command prompt, type the following command\.

```
PS > Set-DefaultAWSRegion -Region us-west-2
```

**Note**  
This setting persists only for the current session\. To apply the setting to all of your PowerShell sessions, add this command to your PowerShell profile as you did for the `Import-Module` command\.

 **To view the current default region for all AWS CLI commands** 

From the PowerShell command prompt, type the following command\.

```
PS > Get-DefaultAWSRegion

Region    Name             IsShellDefault
------    ----             --------------
us-west-2 US West (Oregon) True
```

 **To clear the current default Region for all AWS CLI commands** 

From the PowerShell command prompt, type the following command\.

```
PS > Clear-DefaultAWSRegion
```

 **To view a list of all available AWS Regions** 

From the PowerShell command prompt, type the following command\. The third column in the sample output identifies which Region is the default for your current session\.

```
PS > Get-AWSRegion

Region         Name                      IsShellDefault
------         ----                      --------------
ap-east-1      Asia Pacific (Hong Kong)  False
ap-northeast-1 Asia Pacific (Tokyo)      False
...
us-east-2      US East (Ohio)            False
us-west-1      US West (N. California)   False
us-west-2      US West (Oregon)          True
...
```

**Note**  
Some Regions might be supported but not included in the output of the `Get-AWSRegion` cmdlet\. For example, this is sometimes true of Regions that are not yet global\. If you're not able to specify a Region by adding the `-Region` parameter to a command, try specifying the Region in a custom endpoint instead, as shown in the following section\.

## Specifying a Custom or Nonstandard Endpoint<a name="specifying-a-custom-or-nonstandard-endpoint"></a>

Specify a custom endpoint as a URL by adding the `-EndpointUrl` common parameter to your Tools for Windows PowerShell command, in the following sample format\.

```
PS > Some-AWS-PowerShellCmdlet -EndpointUrl "custom endpoint URL" -Other -Parameters
```

The following is an example using the `Get-EC2Instance` cmdlet\. The custom endpoint is in the `us-west-2`, or US West \(Oregon\) Region in this example, but you can use any other supported AWS Region, including regions that are not enumerated by `Get-AWSRegion`\.

```
PS > Get-EC2Instance -EndpointUrl "https://service-custom-url.us-west-2.amazonaws.com" -InstanceID "i-0555a30a2000000e1"
```