Skip to content
Darrenmkadinali
/
Davil
Public
Code
Issues
Pull requests
Actions
Projects
Wiki
Security
Insights
Settings
Help Panel navigation
Marketplace
Documentation
 / Setup Java JDK
Setup Java JDK
By actions 
 v1.4.4
 1.1k
Set up a specific version of the Java JDK and add the command-line tools to the PATH

View full Marketplace listing
Installation
Copy and paste the following snippet into your .yml file.

Version: v1.4.4 
- name: Setup Java JDK
  uses: actions/setup-java@v1.4.4
  with:
    # The Java version to make available on the path. Takes a whole or semver Java version, or 1.x syntax (e.g. 1.8 => Java 8.x). Early access versions can be specified in the form of e.g. 14-ea, 14.0.0-ea, or 14.0.0-ea.28
    java-version: 
    # The package type (jre, jdk, jdk+fx)
    java-package: # optional, default is jdk
    # The architecture (x86, x64) of the package.
    architecture: # optional, default is x64
    # Path to where the compressed JDK is located. The path could be in your source repository or a local path on the agent.
    jdkFile: # optional
    # ID of the distributionManagement repository in the pom.xml file. Default is `github`
    server-id: # optional, default is github
    # Environment variable name for the username for authentication to the Apache Maven repository. Default is $GITHUB_ACTOR
    server-username: # optional, default is GITHUB_ACTOR
    # Environment variable name for password or token for authentication to the Apache Maven repository. Default is $GITHUB_TOKEN
    server-password: # optional, default is GITHUB_TOKEN
    # Path to where the settings.xml file will be written. Default is ~/.m2.
    settings-path: # optional
    # GPG private key to import. Default is empty string.
    gpg-private-key: # optional
    # Environment variable name for the GPG private key passphrase. Default is $GPG_PASSPHRASE.
    gpg-passphrase: # optional
BreadcrumbsDavil/.github/workflows
/
terraform.yml
in
main

Edit

Preview
Indent mode

Spaces
Indent size

2
Line wrap mode

No wrap
1
# This workflow installs the latest version of Terraform CLI and configures the Terraform CLI configuration file
2
# with an API token for Terraform Cloud (app.terraform.io). On pull request events, this workflow will run
3
# `terraform init`, `terraform fmt`, and `terraform plan` (speculative plan via Terraform Cloud). On push events
4
# to the "main" branch, `terraform apply` will be executed.
5
#
6
# Documentation for `hashicorp/setup-terraform` is located here: https://github.com/hashicorp/setup-terraform
7
#
8
# To use this workflow, you will need to complete the following setup steps.
9
#
10
# 1. Create a `main.tf` file in the root of this repository with the `remote` backend and one or more resources defined.
11
#   Example `main.tf`:
12
#     # The configuration for the `remote` backend.
13
#     terraform {
14
#       backend "remote" {
15
#         # The name of your Terraform Cloud organization.
16
#         organization = "example-organization"
17
#
18
#         # The name of the Terraform Cloud workspace to store Terraform state files in.
19
#         workspaces {
20
#           name = "example-workspace"
21
#         }
22
#       }
23
#     }
24
#
25
#     # An example resource that does nothing.
26
#     resource "null_resource" "example" {
27
#       triggers = {
28
#         value = "A example resource that does nothing!"
29
#       }
30
#     }
31
#
32
#
33
# 2. Generate a Terraform Cloud user API token and store it as a GitHub secret (e.g. TF_API_TOKEN) on this repository.
34
#   Documentation:
35
#     - https://www.terraform.io/docs/cloud/users-teams-organizations/api-tokens.html
36
#     - https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets
37
#
38
# 3. Reference the GitHub secret in step using the `hashicorp/setup-terraform` GitHub Action.
39
#   Example:
40
#     - name: Setup Terraform
41
#       uses: hashicorp/setup-terraform@v1
42
#       with:
43
#         cli_config_credentials_token: ${{ secrets.TF_API_TOKEN }}
44
​
45
name: 'Terraform'
46
​
47
on:
48
  push:
49
    branches: [ "main" ]
50
  pull_request:
51
​
52
permissions:
53
  contents: read
54
​
55
jobs:
56
  terraform:
57
    name: 'Terraform'
58
    runs-on: ubuntu-latest
59
    environment: production
60
​
61
    # Use the Bash shell regardless whether the GitHub Actions runner is ubuntu-latest, macos-latest, or windows-latest
62
    defaults:
63
      run:
64
        shell: bash
65
​
66
    steps:
67
    # Checkout the repository to the GitHub Actions runner
68
    - name: Checkout
Use Control + Space to trigger autocomplete in most situations.
New File at / · Darrenmkadinali/Davil · GitHub 
