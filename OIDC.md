# GitHub Actions, AWS, and Authentication with OIDC.

## Introduction

Especially in project scenarios where a product is based on serverless, cloud-native technologies, Development teams can benefit by leveraging GitHub's hosted runners.

NCI's investment in GitHub Enterprise opens many doors to new and advantageous capabilities as it relates to continuous integration and continuous delivery (CI/CD) tooling. ![GitHub Actions](https://github.com/features/actions) is now available to product teams as a cloud-based CI/CD service, offering an alternative to on-prem based services adopted by the enterprise, such as Jenkins.

As CBIIT's Cloud One environment matures, and as progress to launch and support Cloud Two approaches, Development teams are advancing modern, serverless, and cloud-native products. When evaluating available CI/CD tooling for these modernized architectures, benefits of GitHub actions become obvious for many use cases. GitHub's ![Hosted Runners](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) offers virtual machines to host build, test, and deploy action workflows, following the serverless model. This means that Development and Operations teams do not inherit the overhead of managing the infrastructure (maintenance, upgrades, etc.) for the compute resources consumed to execute actions.

This article focuses on configuring OpenID Connect (OIDC) to authenticate with AWS environments to provision AWS infrastructure defined as code (IaC).

## Background

Credentials are required to be provided by GitHub Actions in order to permit the virtual machine to provision resources in the target AWS account, often as passwords or tokens. Traditional approaches to securing credentials required storing passwords or tokens as secrets in GitHub environments.

NCI Operations teams inherit administrative burden from this traditional approach. For each product hosted in Cloud One, at least two sets of credentials must be created, and managed (manually rotated at least every 90 days). Development teams suffer from delays, which tightly correlate to the growing service backlog of administrative tasks placed on the Operations teams.

CBIIT Development and Operations teams must collaborate to find CI/CD approaches that reduce task overhead and minimize vulnerability exposure to ensure the organization can securely scale to meet the demand of NCI's innovative ecosystem.

## Benefits of Adopting OIDC

Adopting OIDC to enforce secure communications between GitHub and AWS to provision resources is a best practice. The following points outline the benefits achieved by CBIIT through OIDC adoption:

- Reduce administrative overhead by eliminating the burden of rotating credentials. By using OIDC, AWS provides short-lived access tokens that are unique for each workflow run. When GitHub Actions completes a workflow, whether the workflow was successful or unsuccessful, the access tokens expire and must be reissued for the next execution.
- Controlling access by leveraging the AWS' Identity and Access Management (IAM) service for fine-grained access control, a familiar service widely used in today's enterprise. OIDC profiles establish a trust relationship that defines which workflows can retrieve credentials (authentication), and the roles/policies that can be assumed (authorization).
- Hardening security a step further with bypassing the need to exchange secrets between Development and Operations teams when configuring and rotating credentials, and eliminating the need to duplicate credentials with GitHub secrets.

In short, NCI can achieve stronger security posture and work around operational resource constraints with OIDC. Because GitHub offers an OIDC provider, this approach is viable when target environments are hosted in AWS, GCP, or Azure as each of these cloud providers also support OIDC.

## How OIDC Works

## How to Configure OIDC at NCI

## Recommended Changes to Developer IAM Policies

ammending the dev_admin role to allow the 'CreateOpenIDConnectProvider' action under the IAM service. 
