---
title: 指定資料分割和角色部署選項 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d8cb36e4c4475407a122120d8b639f837acb0a0f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>部署指令碼檔案的磁碟分割和角色部署選項
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署精靈會讀取的資料分割和角色部署選項，從\<*專案名稱*> 部署檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]建立此檔案，當您建置[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用資料分割和角色部署選項目前的專案時\<*專案名稱*> 會建立檔案。 如需組態設定的詳細資訊，請參閱 [了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)。  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>檢閱資料分割和角色部署選項  
 中的部署選項\<*專案名稱*> 部署檔案包括下列：  
  
 **資料分割部署選項**  
 \<*專案名稱*> 部署檔案指定目的地資料庫中現有的資料分割會保留或覆寫 （預設值）。 如果保留現有的資料分割，則只會部署新的資料分割，而所有現有的量值群組上的資料分割與彙總設計都會保持不變。  
  
> [!NOTE]  
>  如果刪除存在有資料分割的量值群組，則也會自動刪除資料分割。  
  
 **角色部署選項**  
 \<*專案名稱*> 部署檔案指定下列角色部署選項的其中一個：  
  
-   保留目的地資料庫中之現有的角色和角色成員，僅部署新角色和角色成員。  
  
-   以正在部署的角色和成員取代目的地資料庫中之所有現有的角色和成員。  
  
-   保留目的地資料庫中之現有的角色和角色成員，而且不部署新角色。  
  
-   **注意** ：保留現有角色與成員時，與這些角色相關聯的權限會重設為無。 安全性權限包含在它們所保護的物件中，而非與它們相關聯的安全性角色。 如需如何使用 Analysis Service 部署精靈來處理這項行為的詳細資訊，請參閱 Microsoft 知識庫中的＜保留角色與成員＞。  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>修改資料分割和角色部署選項  
 您可能要部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用不同的資料分割和角色選項所儲存的專案\<*專案名稱*> 部署檔案。 例如，您可能想要保留現有的資料分割、 角色和角色的成員，而不是取代所有現有的資料分割、 角色和成員，如下所示\<*專案名稱*> 部署檔案。  
  
 若要修改的資料分割和角色部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案中，您無法變更專案內的資料分割和角色設定，因為*\<專案名稱 >* **屬性頁面**對話方塊[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]並未顯示這些選項。 如果您想要變更角色和資料分割的部署選項，您必須變更這項資訊內\<*專案名稱*> 部署檔案本身。 下列程序描述如何變更中的資料分割和角色部署選項\<*專案名稱*> 部署檔案。  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>在已產生輸入檔之後，變更資料分割或角色的部署  
  
-   以互動方式執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並在 [Partition and Role Deployment Options (資料分割和角色部署選項)] 頁面上，指定資料分割和角色的新部署選項。  
  
     – 或 –  
  
-   在命令提示字元下執行 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 (如需回應檔案模式的詳細資訊，請參閱 [執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md))。  
  
     – 或 –  
  
-   開啟\<*專案名稱*> 以任何文字編輯器，並手動變更選項。  
  
## <a name="see-also"></a>另請參閱  
 [指定安裝目標](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [指定方案部署的組態設定](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [指定處理選項](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
