# NCI GitHub Actions Operationalization
Product teams across NCI aim to make use of new tooling introduced to the enterprise under the current GitHub Enterprise offering to deploy cloud-hosted applications. As an alternative to Jenkins, GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows automation of build, test, and deployment pipeline processes. 

### The Challenge
While GitHub Actions is an option for product teams within CBIIT, the enterprise needs to determine the path forward with operationalizing the service. Bringing GitHub Actions into CBIITs operational support scope requires governance and process definition. Product Development teams and Operations teams must have a clear picture of responsibilities and process that are in alignment with organizational policy, particularly as it relates to least privilege and separation of duties. 

### The Objective
To efficiently deliver GitHub Actions as a viable product Development teams can leverage for CI/CD within policy and operational constraints. Development teams want to understand the operational team's perspective in what needs to be done to adopt GitHub Actions as a CI/CD product under the support model. The approach is to allow Development teams to perform the research and validate a concept to recommend and allow for feedback from operational teams to determine if the model needs adjustment. Both Development and Operational teams must work together to streamline the adoption process.

### The Scope
This discussion is scoped to how code and infrastructure is built and deployed across environments with regard to tooling. Our attempt is not to change policies, level of privilege, or bypass existing procedures. The discussion is framed around how CBIIT can operationalize a new and available tool, what is proposed with regard to personnel responsibily, and how the proposition aligns with NCI policy.

### The Concept
Development teams are proposing a model that would allow developers to create GitHub Actions workflows that can be leveraged for build, test, and deployment of applications through all tiers. However, only Operations teams would reserve the privilege to deploy to stage and production environments. To enable developers in their efforts to define/validate workflows and execute deployments in lower tiers, we recommend the following structure:
![GitHub Actions Concept Overview](assets/GitHubActionsConceptOverview.png)
The diagram above illustrates the idea that the Operations team can establish a centralized repository that houses the production GitHub Action workflows for all projects. This allows NCI to take advantage of GitHub's predefined roles to limit the privileges that Development teams have to execute deployments in Stage and Production environments. 

Our recommendation is to provide developers to assume a "write" role to be able to maintain workflow definitions and request workflow executions. Operations teams assume the "admin" role, which allows members to create GitHub environments, manage environment secrets, create deployment review checkpoints, and execute deployment workflows. This recommendation ( 1 ) reduces the Operations team workload in creating deployment pipelines; ( 2 ) puts responsibility on developers to correctly configure workflow jobs; and ( 3 ) preserves separation of duty and least privilege to comply with policy. For more about GitHub repository roles, please [click here](https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories/repository-roles-for-an-organization).

### The Details (under construction!)
- This section is to highlight how GitHub Actions enables cross-repository access from the Centralized Operations Repository to the various Project Repositories.
- This is what enables us to achieve NCI policy compliance, as well as DevOps best practices with respect to "build once, deploy many"
- There are three primary inputs to establish a workflow in the centralized operations repo. We've already discussed workflow definitions, and how it is the responsibility of the development team to clone/modify those in the centralized opps repo. The other two inputs are ( 1 ) project code, which includes scripts, IaC templates, etc.; and ( 2 ) build artifacts from the build workflow that is executed in project repositories.
- Thoughts on discussing that developers choose how to authorize with target environements/accounts (secrets manager, OIDC)? These should be provided in service request ticket instructions.
- Dont forget to mention that the diagram below represents the flow between one project and the centralized repo.

![Technical Detail of GitHub Actions Concept](assets/GitHubActionsConceptDetails.png)

### The Process (under construction!)
this is where we spell out that the deployment process remains the same - we submit a ticket through ServiceNow, providing instructions and input parameters. 
We also need to discuss the process for setting up GitHub environments.

### The Responsibilities (under construction!)
just to make things black and white, we can create a table that distinguishes who is responsible for what.
