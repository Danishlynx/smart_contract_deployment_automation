# Smart Contract Deployment Automation

This project focuses on the automation of the deployment of smart contracts currently focusing on a limted set of use cases.

The use cases currently addressed by this project are as follows:

 - Simple Smart Contracts
 - Upgradeable Smart Contracts (using Transparent Proxy pattern)

### File Structure 
This project is primarily following the default hardhat file structure with a few additional directories.

##### Default Directories
+ `Contracts/` - The `.sol` files containing the contracts must be placed in this directory by default according the the hardhat file structure. 

##### Additional Directories

+ `deploy_normalContract/` - The `.js` file containing logic to deploy the normal smart contract will be placed in this directory.
+ `deploy_Implementation_Proxy/` - The `.js` file containing logic to deploy the implementation contract along with the proxy contract will be placed in this directory.
+ `deploy_Upgrade/` - The `.js` file containing logic to deploy the new implementation and point the proxy to it will be placed in this direcotory.

### Setup
Create a repository secret `PRIVATE_KEY` and provide the private key of the wallet that will be used to run the deployment and upgrade transactions.

### Execution 
There are 3 actions that can be performed by the workflows created to cover the 2 use cases mentioned earlier.

1. The deployment of a non-upgradeable simple smart contract.
2. Deploy the implementation contract and the transparent pattern proxy.
3. Deploy the new implementation contract and point the proxy to it.

### Contribution Guideline

1. Create a new branch following this convention below:
- `<type>/<description>`

Type can be `feat, fix, chore` etc. 

Example: `feat/summary-of-your-feature`

2. Apply changes and commit to the branch you created.

3. Create a Pull Request to the target branch, set yourself as assignee and add proper reviewers as part of the secure review process.

##### Volta
For volta net work, the user can create a pull request to merge the branch they created into `volta` branch and upon the merging and closure of the PR, the workflow will be triggered based on what directory the changes were made to and only that particiular action will be performed. 

##### EWC
The process is the same for `ewc` branch, a pull request can be created to merge `volta` into `ewc`, however the workflows will not be automatically triggered, but rather manually triggered by the user.

This proposed workflow for promoting smart contracts from testing stage (Volta) to the production envirment (EWC) ensures that the same code that was tested on testnet is deployed onto the mainnet.

##### Example Execution Steps (Simple Smart Contract)
1. Create a new branch with proper convention.
2. Place the contract inside `Contracts/` directory.
3. Place the `.js` file with the deployment logic inside the `deploy_normalContract/` directory.
4. Ensure the other directories `deploy_Implementation_Proxy/` and `deploy_Upgrade/` are empty and contain no `.js`  files. 
5. Commit and push to the branch you created.
6. Create a pull request to merge into `volta` branch.

Once the pull request is merged and closed, the workflow will trigger for the relevant action which in this case is the simple smart contract deployment.

##### Example Execution Steps (Deploy Implementation and Proxy)
1. Create a new branch with proper convention.
2. Place the contract inside `Contracts/` directory.
3. Place the `.js` file with the deployment logic inside the `deploy_Implementation_Proxy/` directory.
4. Ensure the other directories `deploy_normalContract/` and `deploy_Upgrade/` are empty and contain no `.js`  files. 
5. Commit and push to the branch you created.
6. Create a pull request to merge into `volta` branch.
- Note: In case of future upgrades, you will need to save the proxy address from the workflow logs.

##### Example Execution Steps (Upgrade proxy)
1. Create a new branch with proper convention.
2. Place the new contract inside `Contracts/` directory.
3. Add the new contract name and previous proxy address to the `js` file containing the logic.
3. Place the `.js` file with the deployment logic inside the `deploy_Upgrade/` directory.
4. Ensure the other directories `deploy_normalContract/` and `deploy_Upgrade/` are empty and contain no `.js`  files. 
5. Commit and push to the branch you created.
6. Create a pull request to merge into `volta` branch.


### Future Considerations
This project only covers the normal smart contract deployment and the transparent proxy pattern deployment, however there are multiple proxy patterns such as the UUPS, Diamond and Beacon etc. which are not covered and remain as a consideration for the future.
