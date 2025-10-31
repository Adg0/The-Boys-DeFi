<p align="center">
  <img src="./docs/vaught.png" width="20%" alt="THE BOYS DeFi logo">
</p>
<p align="center">
    <h1 align="center">THE BOYS DeFi</h1>
</p>
<p align="center">
    <em><code>❯ :warning: *This is a proof of concept, not to be used in production environment.*</code></em>
</p>
<p align="center">
	<img src="https://img.shields.io/github/license/Adg0/The-Boys-DeFi?style=flat&logo=opensourceinitiative&logoColor=white&color=0080ff" alt="license">
	<img src="https://img.shields.io/github/last-commit/Adg0/The-Boys-DeFi?style=flat&logo=git&logoColor=white&color=0080ff" alt="last-commit">
	<img src="https://img.shields.io/github/languages/top/Adg0/The-Boys-DeFi?style=flat&color=0080ff" alt="repo-top-language">
	<img src="https://img.shields.io/github/languages/count/Adg0/The-Boys-DeFi?style=flat&color=0080ff" alt="repo-language-count">
</p>
<p align="center">
		<em>Built with the tools and technologies:</em>
</p>
<p align="center">
	<img src="https://img.shields.io/badge/TypeScript-3178C6.svg?style=flat&logo=TypeScript&logoColor=white" alt="TypeScript">
	<img src="https://img.shields.io/badge/React-61DAFB.svg?style=flat&logo=React&logoColor=black" alt="React">
	<img src="https://img.shields.io/badge/Vite-646CFF.svg?style=flat&logo=Vite&logoColor=white" alt="Vite">
	<img src="https://img.shields.io/badge/PostCSS-DD3A0A.svg?style=flat&logo=PostCSS&logoColor=white" alt="PostCSS">
	<img src="https://img.shields.io/badge/YAML-CB171E.svg?style=flat&logo=YAML&logoColor=white" alt="YAML">
</p>

<br>

##### Table of Contents

- [ Overview](#overview)
- [ Features](#features)
- [ Repository Structure](#repository-structure)
- [ Getting Started](#getting-started)
  - [ Prerequisites](#prerequisites)
  - [ Installation](#installation)
  - [ Usage](#usage)
  - [ Tests](#tests)
- [ Project Roadmap](#project-roadmap)
- [ Contributing](#contributing)
- [ License](#license)

---

## Overview

<p>
The Boys is an onchain DeFi borrow/lend platform.

Borrowers are incentivized with Compound-V token.

The utility of Compound-V token is a share of protocol revenue.

The project is implemented using Borrow vaults, HTS and HSCS.</p>

---

## Repository Structure

```sh
└── The-Boys-DeFi/
    ├── README.md
    ├── contracts
    │   ├── asset_lib
    │   ├── comp-v
    │   ├── lending-market
    │   ├── oracle
    │   └── oracle_lib
    ├── docs
    │   ├── ...
    ├── frontend
    │   ├── .gitignore
    │   ├── README.md
    │   ├── components.json
    │   ├── eslint.config.js
    │   ├── images
    │   ├── index.html
    │   ├── package-lock.json
    │   ├── package.json
    │   ├── postcss.config.js
    │   ├── public
    │   ├── src
    │   ├── tailwind.config.js
    │   ├── tsconfig.app.json
    │   ├── tsconfig.json
    │   ├── tsconfig.node.json
    │   └── vite.config.ts
    └── services
        ├── claim
        ├── feeConverter
        └── vault-indexer
```

---

## Getting Started

### Prerequisites

**Node**: `v20.12.2`

### Installation

Build the project from source:

1. Clone the The-Boys-DeFi repository:

```sh
❯ git clone https://github.com/Adg0/The-Boys-DeFi
```

2. Navigate to the project directory:

```sh
❯ cd The-Boys-DeFi
```

3. Run Makefile:

```sh
❯ make
```

### Usage

To run the project, execute the following command:

```sh
❯ make build_frontend
```

### Tests

Execute the test suite using the following command:

```sh
❯ make test
```

---

## Project Roadmap

- [x] **`Milestone 1`**: <strike>Complete and Integrate contract codes with frontend.</strike>
- [ ] **`Milestone 2`**: Launch on Mainnet and start minting Compound-V tokens.

---

## Contributing

Contributions are welcome! Here are several ways you can contribute:

- **[Report Issues](https://github.com/Adg0/The-Boys-DeFi/issues)**: Submit bugs found or log feature requests for the `The-Boys-DeFi` project.
- **[Submit Pull Requests](https://github.com/Adg0/The-Boys-DeFi/blob/main/CONTRIBUTING.md)**: Review open PRs, and submit your own PRs.
- **[Join the Discussions](https://github.com/Adg0/The-Boys-DeFi/discussions)**: Share your insights, provide feedback, or ask questions.

<details closed>
<summary>Contributing Guidelines</summary>

1. **Fork the Repository**: Start by forking the project repository to your github account.
2. **Clone Locally**: Clone the forked repository to your local machine using a git client.
   ```sh
   git clone https://github.com/Adg0/The-Boys-DeFi
   ```
3. **Create a New Branch**: Always work on a new branch, giving it a descriptive name.
   ```sh
   git checkout -b new-feature-x
   ```
4. **Make Your Changes**: Develop and test your changes locally.
5. **Commit Your Changes**: Commit with a clear message describing your updates.
   ```sh
   git commit -m 'new: Implemented new feature x.'
   ```
6. **Push to github**: Push the changes to your forked repository.
   ```sh
   git push origin new-feature-x
   ```
7. **Submit a Pull Request**: Create a PR against the original project repository. Clearly describe the changes and their motivations.
8. **Review**: Once your PR is reviewed and approved, it will be merged into the main branch. Congratulations on your contribution!
</details>

<details closed>
<summary>Contributor Graph</summary>
<br>
<p align="left">
   <a href="https://github.com{/Adg0/The-Boys-DeFi/}graphs/contributors">
      <img src="https://contrib.rocks/image?repo=Adg0/The-Boys-DeFi">
   </a>
</p>
</details>

---

## Features

### Fee converter

Protocols in decentralised finance (DeFi) often generate revenues by accruing fees across a range of markets in a variety of different asset types. The default behaviour of the protocol will typically be to hold all these asset types on the protocol’s balance sheet as protocol-owned liquidity (POL). However, this will often be a suboptimal use of accrued fees.

#### Dutch Auction

The mechanism involves a Dutch auction where the price starts high and decreases over time. The first person to pay the auction price at a certain point is allowed to claim all the assets in the treasury. 

![dutch-auction][def0]

#### Equation

Initial price starts high and as time passes the price drops by a factor of the maximum period(epochPeriod).

$$ price = initPrice - initPrice * timePassed / epochPeriod $$

### Gallery

![Vault][def1]
![Borrowing Flow][def2]
![Liquidation Flow][def3]
![Temp-V][def4]

[def]: ./docs/compv.png
[def1]: ./docs/vault.png
[def2]: ./docs/borrow.png
[def3]: ./docs/liquidation.png
[def4]: ./docs/tempv.png

---

## License

This project is `unlicense` License. For more details, refer to the [LICENSE](https://choosealicense.com/licenses/unlicense/) file.

---
