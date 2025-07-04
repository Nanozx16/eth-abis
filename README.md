# eth-abis

ETH ABIs
Node module to export the following ABIs:

ERC20: Token Standard
ERC721: Non-Fungible Token Standard
ERC1155: Multi Token Standard
FiatTokenV2
Requires the web3 API to be available, either by initializing it yourself, or using a web3-injecting Javascript environment, like MetaMask, Geth, or Mist.

Installation
yarn add @metamask/metamask-eth-abis

or

npm install @metamask/metamask-eth-abis

Usage
let { abiERC20 } = require('metamask-eth-abis');

// ERC 20

let erc20Token = web3.eth.contract(abiERC20).at(contractAddress);

erc20Token.name.call(function (err, name) {
  if (err) {
    console.log(err);
  }
  if (name) {
    console.log('The token name is: ' + name);
  }
});

erc20Token.symbol.call({ from: addr }, function (err, symbol) {
  //ABI expects string here,
  if (err) {
    console.log(err);
  }
  console.log('Token symbol: ' + symbol);
});
Contributing
Setup
Install Node.js version 12
If you are using nvm (recommended) running nvm use will automatically choose the right node version for you.
Install Yarn v1
Run yarn setup to install dependencies and run any requried post-install scripts
Warning: Do not use the yarn / yarn install command directly. Use yarn setup instead. The normal install command will skip required post-install scripts, leaving your development environment in an invalid state.
Testing and Linting
Run yarn test to run the tests once. To run tests on file changes, run yarn test:watch.

Run yarn lint to run the linter, or run yarn lint:fix to run the linter and fix any automatically fixable issues.

Release & Publishing
The project follows the same release process as the other libraries in the MetaMask organization. The GitHub Actions action-create-release-pr and action-publish-release are used to automate the release process; see those repositories for more information about how they work.

Choose a release version.

The release version should be chosen according to SemVer. Analyze the changes to see whether they include any breaking changes, new features, or deprecations, then choose the appropriate SemVer version. See the SemVer specification for more information.
If this release is backporting changes onto a previous release, then ensure there is a major version branch for that version (e.g. 1.x for a v1 backport release).

The major version branch should be set to the most recent release with that major version. For example, when backporting a v1.0.2 release, you'd want to ensure there was a 1.x branch that was set to the v1.0.1 tag.
Trigger the workflow_dispatch event manually for the Create Release Pull Request action to create the release PR.

For a backport release, the base branch should be the major version branch that you ensured existed in step 2. For a normal release, the base branch should be the main branch for that repository (which should be the default value).
This should trigger the action-create-release-pr workflow to create the release PR.
Update the changelog to move each change entry into the appropriate change category (See here for the full list of change categories, and the correct ordering), and edit them to be more easily understood by users of the package.

Generally any changes that don't affect consumers of the package (e.g. lockfile changes or development environment changes) are omitted. Exceptions may be made for changes that might be of interest despite not having an effect upon the published package (e.g. major test improvements, security improvements, improved documentation, etc.).
Try to explain each change in terms that users of the package would understand (e.g. avoid referencing internal variables/concepts).
Consolidate related changes into one change entry if it makes it easier to explain.
Run yarn auto-changelog validate --rc to check that the changelog is correctly formatted.
Review and QA the release.

If changes are made to the base branch, the release branch will need to be updated with these changes and review/QA will need to restart again. As such, it's probably best to avoid merging other PRs into the base branch while review is underway.
Squash & Merge the release.

This should trigger the action-publish-release workflow to tag the final release commit and publish the release on GitHub.
Publish the release on npm.

Be very careful to use a clean local environment to publish the release, and follow exactly the same steps used during CI.
Use npm publish --dry-run to examine the release contents to ensure the correct files are included. Compare to previous releases if necessary (e.g. using https://unpkg.com/browse/[package name]@[package version]/).
Once you are confident the release contents are correct, publish the release using npm publish.
