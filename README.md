# Password Restarter UiPath Project 🚀

This repository is a UiPath automation built on the REFramework (Robotic Enterprise Framework). It automates password restart/credential workflows and is organized into framework and process workflows.

## Quick links (open these in UiPath Studio)
- [Main.xaml](Main.xaml) — Entry point for the project
- [Sontu's Play.xaml](Sontu's%20Play.xaml) — sample/playground workflow
- [project.json](project.json) — project configuration
- [Config.xlsx](Config.xlsx) — external configuration (used by framework)
- [10. Framework/](10.%20Framework/) — framework workflows and helpers
  - [`Framework.InitiAllSettings`](10.%20Framework/InitiAllSettings.xaml)
  - [`Framework.GetAppCredential`](10.%20Framework/GetAppCredential.xaml)
  - [`Framework.InitiAllApplications`](10.%20Framework/InitiAllApplications.xaml)
  - [`Framework.GetTransactionData`](10.%20Framework/GetTransactionData.xaml)
  - [`Framework.SetTransactionStatus`](10.%20Framework/SetTransactionStatus.xaml)
  - [`Framework.CloseAllApplications`](10.%20Framework/CloseAllApplications.xaml)
- [20. ProcessWorkFlows/](20.%20ProcessWorkFlows/) — process-specific workflows
  - [`Process.Process`](20.%20ProcessWorkFlows/Process.xaml)
- [.entities/EntitiesStore.json](.entities/EntitiesStore.json)
- [.local/ProjectSettings.json](.local/ProjectSettings.json)
- [README.md](README.md) — this file

## How it works (high level)
1. INITIALIZE PROCESS
   - [`Framework.InitiAllSettings`](10.%20Framework/InitiAllSettings.xaml) — loads Config.xlsx and assets
   - [`Framework.GetAppCredential`](10.%20Framework/GetAppCredential.xaml) — retrieves credentials (Orchestrator assets / Windows Credential Manager)
   - [`Framework.InitiAllApplications`](10.%20Framework/InitiAllApplications.xaml) — starts and logs into target applications

2. GET TRANSACTION DATA
   - [`Framework.GetTransactionData`](10.%20Framework/GetTransactionData.xaml) — pulls transactions (Orchestrator queue by default) based on Config("OrchestratorQueueName")

3. PROCESS TRANSACTION
   - [`Process.Process`](20.%20ProcessWorkFlows/Process.xaml) — main transaction processing workflow
   - [`Framework.SetTransactionStatus`](10.%20Framework/SetTransactionStatus.xaml) — updates transaction status back to Orchestrator or configured sink

4. END PROCESS
   - [`Framework.CloseAllApplications`](10.%20Framework/CloseAllApplications.xaml) — closes or logs out of applications and performs cleanup

## Getting started / For new projects
1. Edit [Config.xlsx](Config.xlsx) to add or customize required fields (Orchestrator queue name, application paths, credentials keys).
2. Implement or adapt [`Framework.InitiAllApplications`](10.%20Framework/InitiAllApplications.xaml) and [`Framework.CloseAllApplications`](10.%20Framework/CloseAllApplications.xaml) to match target applications.
3. Implement transaction retrieval and status update:
   - [`Framework.GetTransactionData`](10.%20Framework/GetTransactionData.xaml)
   - [`Framework.SetTransactionStatus`](10.%20Framework/SetTransactionStatus.xaml)
4. Implement process logic in [`Process.Process`](20.%20ProcessWorkFlows/Process.xaml) and invoke any supporting workflows.
5. Open [Main.xaml](Main.xaml) in UiPath Studio and run or debug.


## Troubleshooting
- Check execution logs produced by the REFramework (see Main.xaml execution output).
- If workflows fail to open or reference activities, confirm UiPath Studio/Robot versions and packages in [project.json](project.json).
