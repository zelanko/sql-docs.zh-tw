---
title: "建立部署公用程式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "部署封裝 [Integration Services], 部署公用程式"
  - "部署公用程式 [Integration Services]"
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# 建立部署公用程式
  部署封裝的第一步是建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的部署公用程式。 部署公用程式是一個資料夾，包含在其他伺服器的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案中部署封裝所需的檔案。 部署公用程式在儲存 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的電腦上建立。  
  
 建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案之封裝部署公用程式的方法是先設定建立部署公用程式的建立程序，然後再建立專案。 建立專案時，會自動併入專案中所有的封裝和封裝組態。 若要部署專案的其他檔案 (例如讀我檔案)，請將檔案放置在 **專案的** [Miscellaneous] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料夾中。 建立專案時，會自動併入這些檔案。  
  
 您可以不同的方式設定每一個專案部署。 在建立專案和建立封裝部署公用程式之前，您可以設定部署公用程式上的屬性，以自訂在專案中部署封裝的方式。 例如，可以指定在部署專案時是否可以更新封裝組態。 若要存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的屬性，請以滑鼠右鍵按一下專案，然後按一下 [屬性]。  
  
 下表列出部署公用程式屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|AllowConfigurationChange|指定部署期間是否可以更新組態的值。|  
|[CreateDeploymentUtility]|指定建立專案時是否建立封裝部署公用程式的值。 此屬性必須為 **True** ，才能建立部署公用程式。|  
|DeploymentOutputPath|與部署公用程式之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案相關的位置。|  
  
 建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案時，會建立資訊清單檔 \<專案名稱>.SSISDeploymentManifest.xml，以及專案封裝和封裝相依性的副本，並將資訊清單檔和這些副本加入專案的 bin\Deployment 資料夾，或加入 DeploymentOutputPath 屬性指定的位置。 資訊清單檔會列出專案中的封裝、封裝組態和任何其他檔案。  
  
 每次建立專案時，都會重新整理部署資料夾的內容。 這表示系統將會刪除儲存在這個資料夾，而建立程序並未重新複製到資料夾中的任何檔案。 例如，儲存在部署資料夾的封裝組態檔案將會被刪除。  
  
### 建立封裝部署公用程式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含要為其建立封裝部署公用程式之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的方案。  
  
2.  以滑鼠右鍵按一下專案，然後按一下 [屬性]。  
  
3.  在 [\<專案名稱> 屬性頁] 對話方塊中，按一下 [部署公用程式]。  
  
4.  若要在部署封裝時更新封裝組態，請將 **[AllowConfigurationChanges]** 設為 **True**。  
  
5.  將 **[CreateDeploymentUtility]** 設為 **True**。  
  
6.  選擇性地修改 **DeploymentOutputPath** 屬性，以更新部署公用程式的位置。  
  
7.  按一下 **[確定]**。  
  
8.  在方案總管中，以滑鼠右鍵按一下專案，然後按一下 [建立]。  
  
9. 檢視 **[輸出]** 視窗中的建立進度和建立錯誤。  
  
## 請參閱＜  
 [封裝組態](../../integration-services/packages/package-configurations.md)   
 [建立封裝組態](../../integration-services/packages/create-package-configurations.md)   
 [使用部署公用程式來部署封裝](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)   
 [舊版封裝部署 &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)  
  
  