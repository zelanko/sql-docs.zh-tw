---
title: 指定解決方案部署的配置設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8addba32560e136f68e538240f4fce01f826355e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075270"
---
# <a name="specifying-configuration-settings-for-solution-deployment"></a>指定方案部署的組態設定
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署嚮導會從\<*專案名稱*> .configsettings 檔案中，讀取您在部署腳本中使用的資料分割和角色部署選項。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]當您建立[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案時，會建立這個檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]會使用目前專案的設定值，建立\<*專案名稱*> .configsettings 檔案。  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>檢閱部署的組態設定  
 以下是儲存在\<*專案名稱*> .configsettings 檔案中的設定值：  
  
-   **資料來源連接字串** ：依據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中指定的值，每個資料來源都有連接字串。 在這個檔案中儲存連接字串的其餘部分之前，一定會從字串中移除使用者識別碼和密碼。 不過，如果「部署精靈」直接部署至 Analysis Services 執行個體，您就可以在精靈中加入適當的使用者識別碼和密碼資訊，以便成功處理部署資料庫。 如果「部署精靈」有儲存指令碼，這項連接資訊將不會儲存在部署指令碼本身內。  
  
-   **模擬帳戶** ：此設定會指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在每個資料來源中用來執行陳述式的使用者名稱。 如果沒有指定模擬帳戶， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用其登入帳戶來執行陳述式。 如果直接在資料來源中對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登入帳戶授與使用權限，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之所有資料庫中的所有資料庫管理員，都有透過登入帳戶存取資料來源的權限。 如果指定了使用者帳戶和密碼，則在這個檔案中儲存模擬資訊之前，一定會移除這項資訊。 不過，如果「部署精靈」直接部署至 Analysis Services 執行個體，您就可以在精靈中加入適當的使用者識別碼和密碼資訊，以便成功處理部署資料庫。 如果「部署精靈」有儲存指令碼，這項模擬資訊將不會儲存在部署指令碼本身內。  
  
-   **索引鍵錯誤記錄檔** ：此設定會指定資料庫中每個 Cube、量值群組、資料分割以及維度之索引鍵錯誤記錄檔的檔案名稱與路徑。  
  
-   **儲存位置** ：此設定會指定資料庫中每個 Cube、量值群組以及資料分割的儲存位置。 如果沒有為物件提供任何值，「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈」就會使用物件的預設位置。 例如，資料分割使用量值群組的位置、量值群組使用 Cube 的位置、而 Cube 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之物件的預設位置。 此儲存位置可以是本機或通用命名慣例 (UNC) 路徑。  
  
-   **報表伺服器** ：此設定會指定資料庫中內，每個 Cube 中定義之每個報表動作的報表伺服器和資料夾位置。  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>修改部署的組態設定  
 在某些情況下，您可能需要使用不同[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]于\<*專案名稱*> .configsettings 檔案中儲存的設定，來部署專案。 例如，您可能需要變更一個或多個資料來源的連接字串，或為特定的資料分割或量值群組指定儲存位置。  
  
 若要在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案中修改資料分割和角色的部署，您必須在\<*專案名稱*> .configsettings 檔案中變更這項資訊，如以下程式所述。 您無法變更專案內的資料分割和角色設定，因為中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [ * \<專案名稱]>* [**屬性頁面**] 對話方塊並未顯示這些選項。  
  
> [!NOTE]  
>  組態設定可以套用至所有物件，或僅套用至新建立的物件。 唯有將其他物件部署到先前部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，而且不想要覆寫現有的物件時，才會將組態設定套用至新建立的物件。 若要指定設定設定是否要套用至所有物件，或僅套用至新建立的，請\<在*專案名稱*> d 檔案中設定此選項。 如需詳細資訊，請參閱 [指定資料分割和角色部署選項](deployment-script-files-partition-and-role-deployment-options.md)。  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>在已產生輸入檔之後，變更組態設定  
  
-   以互動方式執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並在 [組態設定]**** 頁面上，指定正在部署之物件的組態設定。  
  
     -或-  
  
-   在命令提示字元下執行 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 如需回應檔案模式的詳細資訊，請參閱 [執行 Analysis Services 部署精靈](running-the-analysis-services-deployment-wizard.md)。  
  
     -或-  
  
-   \<使用任何文字編輯器來修改*專案名稱*> .configsettings 檔案。  
  
## <a name="see-also"></a>另請參閱  
 [指定安裝目標](deployment-script-files-specifying-the-installation-target.md)   
 [指定資料分割和角色部署選項](deployment-script-files-partition-and-role-deployment-options.md)   
 [指定處理選項](deployment-script-files-specifying-processing-options.md)  
  
  
