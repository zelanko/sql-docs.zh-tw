---
title: SQL Server Integration Services DevOps 概觀 | Microsoft Docs
description: 了解如何使用 SSIS DevOps 工具建置 SSIS CICD。
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a1f903d0be82d6f5057af68dce80bda1e48238a
ms.sourcegitcommit: 951740963d5fe9cea7f2bfe053c45ad5d846df04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225923"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>SQL Server Integration Services (SSIS) DevOps 工具 (預覽)

[SSIS DevOps 工具](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)延伸模組可在 **Azure DevOps** Marketplace 中取得。

如果您沒有 **Azure DevOps** 組織，請先註冊 [Azure Pipelines ](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops)，然後按照[步驟](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension)新增 **SSIS DevOps 工具**延伸模組。

**SSIS DevOps 工具**包括 **SSIS 建置**工作，以及 **SSIS 部署**發行工作。

- **SSIS 建置**工作支援在專案部署模型或套件部署模型中建置 dtproj 檔案。

- **SSIS 部署**工作支援將單一或多個 ispac 檔案部署到內部部署 SSIS 目錄和 Azure-SSIS IR，或將 SSISDeploymentManifest 檔案及其相關聯的檔案部署到內部部署或 Azure 檔案共用。

## <a name="ssis-build-task"></a>SSIS 建置工作

![建置工作](media/ssis-build-task.png)

### <a name="properties"></a>屬性

#### <a name="project-path"></a>專案路徑

要建置之專案資料夾或檔案的路徑。 如果指定了資料夾路徑，SSIS 建置工作會以遞迴方式搜尋此資料夾下的所有 dtproj 檔案，並建置所有檔案。

專案路徑不能是*空的*，設定為 **.** 以從存放庫的根資料夾建立。

#### <a name="project-configuration"></a>專案組態

要用於建置的專案組態名稱。 如果未提供，則會預設為每個 dtproj 檔案中第一個定義的專案組態。

#### <a name="output-path"></a>輸出路徑

儲存建置結果的個別資料夾路徑，可以透過[發行組建成品工作](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops) \(英文\) 發行為組建成品。

### <a name="limitations-and-known-issues"></a>限制與已知問題

- SSIS 建置工作依賴 Visual Studio 和 SSIS 設計工具，這在建置代理程式上是必要的。 因此，若要在管線中執行 SSIS 建置工作，您必須針對 Microsoft 裝載的代理程式選擇 **vs2017-win2016**，或在自我裝載的代理程式上安裝 Visual Studio 和 SSIS 設計工具 (VS2017 + SSDT2017，或者 VS2019 + SSIS 專案延伸模組)。

- 若要使用任何現成可用的元件 (包括 SSIS Azure Feature Pack 和其他協力廠商元件) 來建置 SSIS 專案，必須在執行管線代理程式的電腦上安裝這些現成可用的元件。  針對 Microsoft 裝載的代理程式，使用者可以在執行 SSIS 建置工作之前，新增 [PowerShell 指令碼工作](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) \(英文\) 或[命令列指令碼工作](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops) \(英文\) 下載並安裝元件。 面下面是可用於安裝 Azure Feature Pack 的範例 PowerShell 指令碼： 

```powershell
wget -Uri https://download.microsoft.com/download/E/E/0/EE0CB6A0-4105-466D-A7CA-5E39FA9AB128/SsisAzureFeaturePack_2017_x86.msi -OutFile AFP.msi

start -Wait -FilePath msiexec -Args "/i AFP.msi /quiet /l* log.txt"

cat log.txt
```

- 在 SSIS 建置工作中不支援 **EncryptSensitiveWithPassword** 和 **EncryptAllWithPassword** 的保護層級。 確定程式碼基底中的所有 SSIS 專案都不是使用這兩個保護層級，否則 SSIS 建置工作會在執行期間停止回應並逾時。

- **ConnectByProxy** 是最近在 SSDT 中新增的屬性。 Microsoft 裝載的代理程式上安裝的 SSDT 未更新，因此請使用自我裝載的代理程式作為因應措施。

## <a name="ssis-deploy-task"></a>SSIS 部署工作

![部署工作](media/ssis-deploy-task.png)

### <a name="properties"></a>屬性

#### <a name="source-path"></a>來源路徑

您想要部署的來源 ISPAC 或 SSISDeploymentManifest 檔案的路徑。 這個路徑可以是資料夾路徑或檔案路徑。

#### <a name="destination-type"></a>目的地類型

目的地類型。 目前的 SSIS 部署工作支援兩種類型：

- *檔案系統*：將 SSISDeploymentManifest 檔案及其相關聯的檔案部署至指定的檔案系統。 支援內部部署和 Azure 檔案共用。
- *SSISDB*：將 ISPAC 檔案部署到指定的 SSIS 目錄，其可裝載於內部部署 SQL Server 或 Azure-SSIS Integration Runtime 上。

#### <a name="destination-server"></a>目的地伺服器

目的地 SQL Server 的名稱。 它可以是內部部署 SQL Server、Azure SQL Database 或 Azure SQL Database 受控執行個體的名稱。 只有當目的地類型為 SSISDB 時，才會顯示此屬性。

#### <a name="destination-path"></a>目的地路徑

將在其中部署來源檔案的目的地資料夾路徑。 例如：

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

SSIS 部署工作將會建立資料夾與子資料夾 (如果不存在)。

#### <a name="authentication-type"></a>驗證類型

用來存取指定目的地伺服器的驗證類型。 只有當目的地類型為 SSISDB 時，才會顯示此屬性。 一般 SSIS 部署工作支援四種類型：

- Windows 驗證
- SQL Server 驗證
- Active Directory - 密碼
- Active Directory - 整合式

但是，是否支援特定的驗證類型取決於目的地伺服器類型和代理程式類型。 詳細資料支援矩陣會列在下表中。

| |Microsoft 裝載的代理程式|自我裝載的代理程式|
|---------|---------|---------|
|SQL Server 內部部署或 VM |N/A|Windows 驗證|
|Azure SQL|SQL Server 驗證 <br> Active Directory - 密碼|SQL Server 驗證 <br> Active Directory - 密碼 <br> Active Directory - 整合式|

#### <a name="domain-name"></a>網域名稱

用來存取指定檔案系統的網域名稱。 只有當目的地類型為 [檔案系統] 時，才會顯示此屬性。
當執行自我裝載代理程式的使用者帳戶已被授與指定目的地路徑的讀取/寫入存取權時，您可以將它保留空白。

#### <a name="username"></a>使用者名稱

存取指定檔案系統或 SSISDB 的使用者名稱。 當目的地類型為 [檔案系統] 或驗證類型為 [SQL Server 驗證] 或 [Active Directory - 密碼] 時，就會顯示此屬性。
當目的地類型為 [檔案系統]，而執行自我裝載代理程式的使用者帳戶已被授與指定目的地路徑的讀取/寫入存取權時，您可以將它保留空白。

#### <a name="password"></a>密碼

用來存取指定檔案系統或 SSISDB 的密碼。 當目的地類型為 [檔案系統] 或驗證類型為 [SQL Server 驗證] 或 [Active Directory - 密碼] 時，就會顯示此屬性。
當目的地類型為 [檔案系統]，且執行自我裝載代理程式的使用者帳戶已被授與指定目的地路徑的讀取/寫入存取權時，您可以將它保留空白。

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>覆寫相同名稱的現有專案或 SSISDeploymentManifest 檔案

指定是否覆寫相同名稱的現有專案或 SSISDeploymentManifest 檔案。 如果為 [否]，SSIS 部署工作會略過部署這些專案或檔案。

#### <a name="continue-deployment-when-error-occurs"></a>發生錯誤時繼續部署

指定在發生錯誤時，tp 是否繼續部署剩餘的專案或檔案。 如果為 [否]，則會在發生錯誤時立即停止 SSIS 部署工作。

### <a name="limitations-and-known-issues"></a>限制與已知問題

SSIS 部署工作目前不支援下列情節：

- 在 SSIS 目錄中設定環境。
- 將 ispac 部署至 Azure SQL Server 或 Azure SQL 受控執行個體，這只允許多重要素驗證 (MFA)。
- 將套件部署到 MSDB 或 SSIS 封裝存放區。

## <a name="release-notes"></a>版本資訊

### <a name="version-013-preview"></a>0\.1.3 版預覽

發行日期：2020 年 1 月 19 日

- 已修正當 ispac 的原始檔案名稱變更時即無法部署的問題。

### <a name="version-012-preview"></a>0\.1.2 版預覽

發行日期：2020 年 1 月 13 日

- 新增了更詳細的例外狀況資訊，當目的地類型為 SSISDB 時，會顯示在 SSIS 部署工作記錄中。
- 修正了 SSIS 部署工作中，目的地路徑屬性說明文字的範例目的地路徑。

### <a name="version-011-preview"></a>0\.1.1 版預覽

發行日期：2020 年 1 月 6 日

- 新增了最低代理程式版本需求的限制。 目前，此產品的最低代理程式版本是 2.144.0。
- 修正了 SSIS 部署工作的部分錯誤顯示文字。
- 修正部分錯誤訊息。

### <a name="version-010-preview"></a>0\.1.0 版預覽

發行日期：2019 年 12 月 5 日

SSIS DevOps 工具的初始版本。 這是預覽版本。

## <a name="next-steps"></a>後續步驟

- 取得 [SSIS DevOps 延伸模組](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)
