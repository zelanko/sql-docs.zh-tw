---
title: 使用部署參與者自訂資料庫部署
description: 了解如何修改資料庫物件的行為。 檢視建置和部署參與者的資源，以及查看使用這些資源的案例範例。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 4ca036a22497f05141a7777ddb00ac6ca53dab84
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987774"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>使用組建和部署參與者自訂資料庫建置和部署

Visual Studio 提供可用來修改資料庫專案建置和部署動作行為的擴充點。  
  
## <a name="available-extensibility-points"></a>可用的擴充點  
您可以建立擴充點的擴充功能，如下表所示：  
  
|**動作**|**參與者型別**|**注意事項**|  
|--------------|------------------------|-------------|  
|Build|BuildContributor|SQL 專案建置期間，在完整地驗證專案模型之後，執行這種擴充。 除了建置工作的所有屬性和所有自訂引數之外，建置參與者也可以存取整個模型。|  
|部署|DeploymentPlanModifier|SQL 專案部署期間，在產生部署計畫之後，但在執行部署計畫之前，執行這種擴充當做部署管線的一部分。 您可以使用 DeploymentPlanModifier 透過加入或移除步驟修改部署計畫。 部署參與者可以存取部署計畫、比較結果，以及來源和目標模型。|  
|部署|DeploymentPlanExecutor|當部署計畫執行時執行這種擴充，並針對部署計畫提供唯讀存取。 DeploymentPlanExectutor 會根據部署計畫來執行動作。|  
  
### <a name="supported-extensibility-scenarios"></a>支援的擴充性案例  
您可以實作組建或部署參與者以實現下列範例案例：  
  
-   **專案建置期間產生結構描述文件** - 若要支援這個案例，請實作 [BuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.buildcontributor) 並覆寫 OnExecute 方法以產生結構描述文件。 您可以建立目標檔案，定義可控制擴充功能是否執行及指定輸出檔名稱的預設引數。  
  
-   **當部署 SQL 專案時產生差異報表** - 若要支援這個案例，請實作 [DeploymentPlanExecutor](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentplanexecutor)，以便在部署 SQL 專案時產生 XML 檔案。  
  
-   **修改部署計畫，隨資料異動而變更** - 若要支援這個案例，請實作 [DeploymentPlanModifier](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentplanmodifier) 並且逐一查看部署計畫。 對於該計畫中的每 SqlTableMigrationStep，檢查比較結果，決定應該執行或略過該步驟。  
  
-   **將檔案複製到部署 SQL 專案時產生的 dacpac** - 若要支援這個案例，請實作部署參與者並覆寫 OnEstablishDeploymentConfiguration 方法，以指定由專案系統標示為 DeploymentExtensionConfiguration 的檔案。 這些檔案應複製到輸出資料夾並加入至產生的 dacpac 內部。 您也可以修改參與者，將多個檔案合併至一個新檔案，以便複製到輸出資料夾並加入至部署資訊清單。 在部署期間，您可以實作 OnApplyDeploymentConfiguration 方法，從 dacpac 擷取那些檔案並準備檔案使用於 OnExecute 方法。  
  
此外，您可以從參與者公開寫入資料庫專案檔的自訂名稱/值引數組。 您可以使用這些引數，讓參與者從 MSBuild 擷取資訊或讓參與者的使用者自訂行為。 例如，您可以讓使用者指定輸入或輸出檔的名稱。  
  
## <a name="common-tasks"></a>一般工作  
  
|**一般工作**|**支援內容**|  
|--------------------|--------------------------|  
|**深入了解擴充點：** 您可以了解用來實作組建和部署參與者的基底類別。|[BuildContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.buildcontributor)<br /><br />[DeploymentContributor](/dotnet/api/microsoft.sqlserver.dac.deployment.deploymentcontributor)|  
|**建立範例參與者：** 了解建立組建或部署參與者所需的步驟。 如果遵循這些逐步解說，您會：<br /><br />-   建立組建參與者，以產生列出模型中所有項目的報表。<br />-   建立部署參與者，以便在執行之前變更部署計畫。<br />-   建立部署參與者，以便在部署 SQL 專案時產生部署報表。<br /><br />根據您要如何將參與者散發給小組，可以在單一組件或數個組件中建立所有參與者。|[逐步解說：延伸資料庫專案組建，以產生模型統計資料](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[逐步解說：延伸資料庫專案部署以修改部署計畫](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[逐步解說：延伸資料庫專案部署以分析部署計畫](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>另請參閱  
[定義 SQL 單元測試的自訂條件](/previous-versions/sql/sql-server-data-tools/jj860449(v=vs.103))  
