---
title: 指定資料分割和角色部署選項 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
ms.openlocfilehash: f4f2f5bb2f3f39636541d5aea5b931b1dcc72534
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546860"
---
# <a name="specifying-partition-and-role-deployment-options"></a>指定資料分割和角色部署選項
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署嚮導會從 d 檔案讀取分割區和角色部署選項 \<*project name*> 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]當您建立專案時，會建立這個檔案 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]建立 d 檔案時，會使用目前專案的資料分割和角色部署選項 \<*project name*> 。 如需組態設定的詳細資訊，請參閱 [了解用來建立部署指令碼的輸入檔](deployment-script-files-input-used-to-create-deployment-script.md)。  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>檢閱資料分割和角色部署選項  
 D 檔案中的部署選項 \<*project name*> 包括下列各項：  
  
 **資料分割部署選項**  
 \<*project name*>D 檔案會指定是否保留或覆寫目的地資料庫中的現有資料分割（預設值）。 如果保留現有的資料分割，則只會部署新的資料分割，而所有現有的量值群組上的資料分割與彙總設計都會保持不變。  
  
> [!NOTE]  
>  如果刪除存在有資料分割的量值群組，則也會自動刪除資料分割。  
  
 **角色部署選項**  
 D 檔案會 \<*project name*> 指定下列其中一個角色部署選項：  
  
-   保留目的地資料庫中之現有的角色和角色成員，僅部署新角色和角色成員。  
  
-   以正在部署的角色和成員取代目的地資料庫中之所有現有的角色和成員。  
  
-   保留目的地資料庫中之現有的角色和角色成員，而且不部署新角色。  
  
-   **注意** ：保留現有角色與成員時，與這些角色相關聯的權限會重設為無。 安全性權限包含在它們所保護的物件中，而非與它們相關聯的安全性角色。 如需如何使用 Analysis Services 部署嚮導來處理此行為的詳細資訊，請參閱 Microsoft 知識庫中的「保留角色和成員」。  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>修改資料分割和角色部署選項  
 您可能必須 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用與 d 檔案中儲存的不同分割區和角色選項，來部署專案 \<*project name*> 。 例如，您可能會想要保留現有的分割區、角色和角色成員，而不是取代所有現有的分割區、角色和成員，如 d 檔案中所示 \<*project name*> 。  
  
 若要在專案中修改資料分割和角色的部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您無法變更專案內的資料分割和角色設定，因為中的 [ *\<project name>* **屬性頁面**] 對話方塊 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 並未顯示這些選項。 如果您想要變更角色和分割區的部署選項，您必須在 d 檔案內變更此資訊 \<*project name*> 。 下列程式描述如何變更 d 檔案內的資料分割和角色部署選項 \<*project name*> 。  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>在已產生輸入檔之後，變更資料分割或角色的部署  
  
-   以互動方式執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並在 [Partition and Role Deployment Options (資料分割和角色部署選項)]**** 頁面上，指定資料分割和角色的新部署選項。  
  
     -或-  
  
-   在命令提示字元下執行 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 （如需回應檔案模式的詳細資訊，請參閱執行[Analysis Services 部署嚮導](running-the-analysis-services-deployment-wizard.md)）。  
  
     -或-  
  
-   \<*project name*>在任何文字編輯器中開啟 d，並手動變更選項。  
  
## <a name="see-also"></a>另請參閱  
 [指定安裝目標](deployment-script-files-specifying-the-installation-target.md)   
 [指定解決方案部署的設定](deployment-script-files-solution-deployment-config-settings.md)   
 [指定處理選項](deployment-script-files-specifying-processing-options.md)  
  
  
