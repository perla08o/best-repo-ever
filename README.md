# Salesforce DX Project: Next Steps

Now that you’ve created a Salesforce DX project, what’s next? Here are some documentation resources to get you started.

## How Do You Plan to Deploy Your Changes?

Do you want to deploy a set of changes, or create a self-contained application? Choose a [development model](https://developer.salesforce.com/tools/vscode/en/user-guide/development-models).

## Configure Your Salesforce DX Project

The `sfdx-project.json` file contains useful configuration information for your project. See [Salesforce DX Project Configuration](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ws_config.htm) in the _Salesforce DX Developer Guide_ for details about this file.

## Read All About It

- [Salesforce Extensions Documentation](https://developer.salesforce.com/tools/vscode/)
- [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [Salesforce DX Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [Salesforce CLI Command Reference](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference.htm)

## Branch Naming

| Branch  | Purpose                                                                            | Rule                            | Example                 |
|---------|------------------------------------------------------------------------------------|---------------------------------|-------------------------|
| Feature | New features, tasks, etc.                                                          | `<project_prefix>_<ticket_number>_<short_title>` | `own_75_assign_change_author` |

## Commit Naming

| Rule                            | Example                 |
|---------------------------------|-------------------------|
| `<project_prefix>-<ticket_number>: <title>` | `OWN-75: ability to assign Change Author for Programs Queue` |

## Git flow
PR: Pull Request
<br >CI: Circle CI
<br >** signifies a branch for example: \*staging\*
<br >-- signifies a sandbox for example -dcrstaging-

```mermaid
flowchart TB
    A(Merge *staging* to *dcrdev#*) --> R(CI deploy to -dcrdev#- )
    R --> B(Creating new feature branch from *staging*)
    B -->|own_75_assign_change_author| C(Commit changes and Push to *feature* )
    C --> W(Push commit to *dcrdev#* \n using command:\ngit push origin own_75_assign_change_author:dcrdev#)
    W --> T(CI runs tests and deploys to -dcrdev#- )
    T --> O(Finally test changes on -dcrdev#- )
    O --> D(Create PR of *feature branch* to *staging* \n Select reviewer \nskip this if a pull request was already created before)
    D --> E(Send PR to review)
    E -->|PR Approved| F1(Merge PR to *staging*)
    F1 -->G(CI deploys *staging* to -dcrstaging- )
    E -->|PR Rejected| F2(Make code changes)
    F2 --> C
    G --> H(Testing on -dcrstaging- )
    H --> |QA ok|J1(Merge *staging* to *uat*)
    H --> |QA reopen|F2
    J1 --> L(CI deploy *uat* to -dcruat- )
