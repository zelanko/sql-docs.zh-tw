---
title: 部署模型 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 58f946f89691a6e26ba4402166b8ad725e7a977c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761780"
---
# <a name="deploying-models-master-data-services"></a>部署模型 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中的套件是一個 XML 檔案，其中包含可部署的模型結構，以及模型中的資料 (選擇性)。 使用模型封裝將模型的副本從一個 MDS 環境移到另一個 MDS 環境，或在現有的 MDS 環境中建立新的模型。  
  
> [!IMPORTANT]  
>  封裝只能部署到之前建立封裝所使用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 這表示，在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中建立的套件無法部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 或更高版本。  
  
## <a name="tools-for-deploying-models"></a>部署模型的工具  
 若要使用模型封裝，您可以使用以下三個工具之一，端視您的需要而定。  
  
-   **MDSModelDeploy 工具**:若要建立及部署模型物件和資料，請使用 MDSModelDeploy.exe 工具。 如果您在安裝 MDS 時選取的預設路徑，此工具位於*磁碟機*: \Program Files\Microsoft SQL Server\120\Master Data services\configuration。  
  
-   **模型部署精靈**:若要建立及部署的模型結構的封裝，使用中的精靈[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]web 應用程式。 您無法使用此精靈來部署資料。  
  
-   **模型封裝編輯器**:若要編輯模型封裝，請使用 ModelPackageEditor.exe 以啟動 「 模型封裝編輯器精靈 」。 您可以使用此精靈編輯 MDSModelDeploy 工具或「模型部署」精靈所建立的封裝。 如果您在安裝 MDS 時選取的預設路徑，此工具位於*磁碟機*: \Program Files\Microsoft SQL Server\120\Master Data services\configuration。  
  
> [!IMPORTANT]  
>  您可以使用 MDSDeployModel 來建立新模型、建立模型的複製或更新現有模型及其資料。 如果您使用 MDSModelDeploy 工具來更新現有模型及其資料，而且封裝不包含存在目的地模型中的實體、屬性或成員，MDSModelDeploy 就不會從模型中刪除該實體、屬性或成員。  
  
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
  
 使用者定義的中繼資料、檔案屬性及使用者和群組的權限不包含在內。 在部署模型之後，您必須手動更新這些項目。  
  
## <a name="sample-packages"></a>範例封裝  
 當您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時，會包含範例封裝檔案。 這些封裝檔案位於 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]安裝位置的 Master Data Services\Samples\Packages 目錄中。 當您使用 MDSModelDeploy 工具部署這些範例封裝時，則會建立範例模型並以資料擴展。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|使用 MDSModelDeploy 工具建立模型物件與/或資料的新部署封裝。|[使用 MDSModelDeploy 建立模型部署封裝](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|使用精靈僅建立模型物件的新部署封裝。|[使用精靈建立模型部署套件](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|使用 MDSModelDeploy 工具部署模型物件與資料的封裝。|[使用 MDSModelDeploy 部署模型部署套件](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|使用精靈僅部署模型物件的封裝。|[使用精靈部署模型部署封裝](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|編輯模型部署封裝以部署選取的模型部分，而非整個模型。|[編輯模型部署封裝](../../2014/master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [模型部署選項 &#40;Master Data Services&#41;](model-deployment-options-master-data-services.md)  
  
  
