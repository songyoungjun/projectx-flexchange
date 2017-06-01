# projectx-flexchange

**Please note that this is a work-in-progress and the repository will be updated over time.**

# Harnessing distributed ledgers to develop a trusted platform for the energy market

## Introduction

Utilidex’s mission is to revolutionise the way customers buy, sell and optimise their energy estate.  The company’s digital platform, known as the Utilidex | Hub is used by a range of participants in the market, including energy generators/prosumers, suppliers and corporates. This customer set of buyers and sellers, working on a common platform, creates a unique opportunity to leverage the power of Blockchains, or distributed ledger, technology to facilitate new types of energy transactions.  In partnership, Utilidex and Microsoft helped develop the start of an enterprise solution that includes the security and trust features needed for practical commercial use.

Utilidex is publishing some of the work they had been doing with Microsoft on Blockchains, as part of their wider initiative to demystify the technology and help with its adoption in energy. This technical report discusses incorporating a Blockchain into an enterprise solution for the energy market. It explores security, deployment, integrating with applications, and user authentication. Read this document to see how a Blockchain can become part of your solution and how Azure services can provide it with the enterprise capabilities needed. Specifically, this document looks at distributed ledgers based on Ethereum Blockchain technology. 

**Our focus was on enterprise capabilities over the underlying Blockchain technology. Ethereum was chosen because it was the best option to work with at the time. The design considerations can apply to any Blockchain implementation.**

Utilidex has been working with Microsoft for several years.  This paper is the outcome of one of the workshops run with Utilidex at Microsoft offices in London between 21 and 24 February 2017. This paper shares our learning to that point in this rapidly developing area. It documents our journey and considerations at that time. We expect that relentless progress will offer alternatives to our approaches. It is the identifying of enterprise requirements that we believe will provide value for readers interested in using this transformational technology. 

## Video Summary

This [video](https://www.youtube.com/watch?v=pCTJ6GF-eNc&feature=youtu.be) describes the outcome of the workshop.

## Technical Report

The full [technical report](https://github.com/Utilidex/projectx-flexchange/blob/master/Harnessing%20distributed%20ledgers%20to%20develop%20a%20trusted%20platform%20for%20the%20energy%20market%20-%20FINAL.pdf) describes many of the considerations and decisions made.
]
## If you would like to look at the source code and scripts

**Given the tight time constraints and the learning journey, the implementation is provided as-is as sample code only for reference. If you decide to build on it, we highly recommend you conduct a full code review and decide if it is usable for your purposes.**

The following are the relevant repositories and what they contain.

Repository | Summary
--- | ---
https://github.com/utilidex/projectx-flexchange | Landing page for all repositories
https://github.com/utilidex/projectx-flexchange-orchestration | Overall orchestration scripts to stand up a new chain or add a member, etc.
https://github.com/utilidex/projectx-flexchange-smart-contract | Solidity EnergyExchange smart contract implementation
https://github.com/utilidex/projectx-flexchange-active-directory | Azure Active Directory configuration instructions.
https://github.com/utilidex/projectx-flexchange-core-apps | Core deployment Web and API Applications.
https://github.com/utilidex/projectx-flexchange-member-apps | Member deployment Web and API Applications.
https://github.com/utilidex/projectx-flexchange-vmss-automation | Automation scripts to start / stop Ethereum nodes.
https://github.com/utilidex/projectx-flexchange-arm-templates | Core ARM templates for Ethereum.
https://github.com/utilidex/projectx-flexchange-dev-vm | DevVm/Jump Box in the Initial Deployment.
https://github.com/utilidex/projectx-flexchange-keystore-backup | Service to backup keystore.
https://github.com/utilidex/projectx-flexchange-client-watchdog | Service to monitor and restart Ethereum Geth clients on stalled nodes.
https://github.com/utilidex/projectx-flexchange-hackfest-images | Docker images for Ethereum Geth nodes. Forked from EthereumEx to add additional services to the image (key backup and monitoring).
https://github.com/utilidex/projectx-flexchange-member-services | ARM template and PS scripts for App Services components in member deployments and integration to existing VNet.
https://github.com/utilidex/projectx-flexchange-build-automation | Scripts to assist in the build and deployment of smart contracts using Truffle

## If you would like to try the solution out

Please follow the setup steps documented in each of the following repositories. They should end with a working solution that demonstrates the approaches from this work.

1. [Deploy the blockchain](https://github.com/utilidex/projectx-flexchange-orchestration)
2. [Migrate the smart contract](https://github.com/utilidex/projectx-flexchange-smart-contract)
3. [Configure Azure Active Directory](https://github.com/utilidex/projectx-flexchange-active-directory)
4. [Install core applications](https://github.com/utilidex/projectx-flexchange-core-apps)
5. [Install member applications](https://github.com/utilidex/projectx-flexchange-member-apps)

## Exercising the solution

### 1/ Testing Azure Active Directory authentication

1. Go to the member application endpoint (e.g. https://webappuu6ihjhahzgna.azurewebsites.net). 
2. Sign in using the link at the top right corner of the page with the user created during core component deployment.

### 2/ Testing the blockchain JSON-RPC interface

1. With a signed-in user, click on Create Account within the member application.
2. Enter an account name (e.g. Solar).
3. Click the Create Account button.

For each successful account creation action, there should be a blockchain address returned for it (e.g. 0x129ad3cb63fa3a2f43a06b7114498d915cb92df9). This should be displayed in the result page, and if you return the the Create Account form.

### 3/ Testing smart contract calls

1. Go to the core application at the endpoint you created and sign-in.
2. In the application, click on the Propose Agreement link at the top of the page.
3. Select appropriate values from the drop down lists. When all selections are complete, click on the Propose Agreement button.

If the proposal is created successfully, it will return "True" in the result page. A false return indicates an error.

4. Additional smart contract calls can be initiated via the member application by using the "Sign an Agreement" and "Check an Agreement's Completion Status" options.

To trace execution and for debugging, set the project to ServerDebug and redeploy. You can then attach to the running instances with the Visual Studio debugger to see what is happening.

### Notes

1. If you encounter the following error, please sign-in again. Sign-out first if necessary.
```
Failed to acquire token silently as no token was found in the cache. Call method AcquireToken 
```
2. If you would like to debug locally then you will need to add localhost addresses to the Reply URL list in the relevant application registrations on Azure Active Directory. E.g. https://localhost:44354/. Changes will also need to be made to the Azure Active Directory configuration values in web.config (e.g. RedirectURL).

# Contributors

With thanks to Abhinav Jain, Mike McCloskey, Munah Brys, Richard Brys, Samir Gupta, Sudhir Gupta, and Vaibhav Mishra from Utilidex; and Ben Roscorla, Gina Dragulin, John Donnelly, Jonathan Collinge, Michael Platt, Mike Ormond and Thomas Conte from Microsoft.
