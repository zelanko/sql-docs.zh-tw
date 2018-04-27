---
title: 部署模型 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
caps.latest.revision: 24
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 198c590933bff5c9d19c00a1238a3f70fb9d84da
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="deploying-models-master-data-services"></a>部署模型 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中的套件是一個 XML 檔案，其中包含可部署的模型結構，以及模型中的資料 (選擇性)。 使用模型封裝將模型的副本從一個 MDS 環境移到另一個 MDS 環境，或在現有的 MDS 環境中建立新的模型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] **MDSModelDeploy 工具** 與在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 或更新版本中建立的舊版套件相容。  
  
## <a name="tools-for-deploying-models"></a>部署模型的工具  
 若要使用模型封裝，您可以使用以下三個工具之一，端視您的需要而定。  
  
-   **MDSModelDeploy 工具**：若要建立與部署模型物件和資料，請使用 MDSModelDeploy.exe 工具。 如果您在安裝 MDS 時選取了預設路徑，此工具會位於 *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration。  
  
-   **模型部署精靈：**若只要建立與部署模型結構的套件，請使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中的精靈。 您無法使用此精靈來部署資料。  
  
-   **模型套件編輯器**：若要編輯模型套件，請使用 ModelPackageEditor.exe 以啟動模型套件編輯器精靈。 您可以使用此精靈編輯 MDSModelDeploy 工具或「模型部署」精靈所建立的封裝。 如果您在安裝 MDS 時選取了預設路徑，此工具會位於 *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration。  
  
> [!IMPORTANT]  
>  您可以使用 MDSModelDeploy 工具建立新的模型、建立模型的複製，或更新現有的模型及其資料。 如果您使用 MDSModelDeploy 工具來更新現有模型及其資料，而且封裝不包含存在目的地模型中的實體、屬性或成員，MDSModelDeploy 就不會從模型中刪除該實體、屬性或成員。  
  
## <a name="what-packages-contain"></a>封裝內容  
 模型封裝是以副檔名 .pkg 儲存的 XML 檔案。 當您建立部署封裝時，可以決定是否要包含資料。 如果決定要包含資料，必須選取要包含的資料版本。  
  
 所有模型物件都會包含在封裝中。 包括下列物件：  
  
-   實體  
  
-   屬性  
  
-   屬性群組  
  
-   階層  
  
-   集合  
  
-   商務規則  
  
-   版本旗標  
  
-   訂閱檢視  
  
 檔案屬性，以及使用者和群組的權限不會包含在內。 在部署模型之後，您必須手動更新這些項目。  
  
## <a name="sample-packages"></a>範例封裝  
 當您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時，會包含範例封裝檔案。 這些封裝檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]安裝位置的 Master Data Services\Samples\Packages 目錄中。 當您使用 MDSModelDeploy 工具部署這些範例封裝時，則會建立範例模型並以資料擴展。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|使用 MDSModelDeploy 工具建立模型物件與/或資料的新部署封裝。|[使用 MDSModelDeploy 建立模型部署封裝](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|使用精靈僅建立模型物件的新部署封裝。|[使用精靈建立模型部署套件](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|使用 MDSModelDeploy 工具部署模型物件與資料的封裝。|[使用 MDSModelDeploy 部署模型部署套件](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|使用精靈僅部署模型物件的封裝。|[使用精靈部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|編輯模型部署封裝以部署選取的模型部分，而非整個模型。|[編輯模型部署封裝](../master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [模型部署選項 &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)  
  
  
