---
title: "指定資料分割和角色部署選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "輸入檔 [Analysis Services]"
  - "分割區 [Analysis Services], 部署選項"
  - "Analysis Services 部署, 角色"
  - "Analysis Services 部署, 分割區"
  - "Analysis Services 部署精靈, 角色"
  - "Analysis Services 部署精靈, 分割區"
  - "部署 [Analysis Services], 角色"
  - "角色 [Analysis Services], 部署選項"
  - "部署 [Analysis Services], 分割區"
  - "修改角色部署"
  - "修改資料分割部署"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 指定資料分割和角色部署選項
  [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 會從 \<*專案名稱*>.deploymentoptions 檔案讀取資料分割和角色部署選項。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會在您建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時建立此檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會在建立 \<*專案名稱*>.deploymentoptions 檔案之後，使用目前專案的資料分割和角色部署選項。 如需組態設定的詳細資訊，請參閱[了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)。  
  
## 檢閱資料分割和角色部署選項  
 \<*專案名稱*>.deploymentoptions 檔案中的部署選項如下：  
  
 **資料分割部署選項**  
 \<*專案名稱*>.deploymentoptions 檔案會指定要保留或覆寫 (預設) 目的地資料庫中的現有分割區。 如果保留現有的資料分割，則只會部署新的資料分割，而所有現有的量值群組上的資料分割與彙總設計都會保持不變。  
  
> [!NOTE]  
>  如果刪除存在有資料分割的量值群組，則也會自動刪除資料分割。  
  
 **角色部署選項**  
 \<*專案名稱*>.deploymentoptions 檔案會指定下列角色部署選項其中之一：  
  
-   保留目的地資料庫中之現有的角色和角色成員，僅部署新角色和角色成員。  
  
-   以正在部署的角色和成員取代目的地資料庫中之所有現有的角色和成員。  
  
-   保留目的地資料庫中之現有的角色和角色成員，而且不部署新角色。  
  
-   **注意**：保留現有角色與成員時，與這些角色相關聯的權限會重設為無。 安全性權限包含在它們所保護的物件中，而非與它們相關聯的安全性角色。 如需如何使用 Analysis Service 部署精靈來處理這項行為的詳細資訊，請參閱 Microsoft 知識庫中的＜保留角色與成員＞。  
  
## 修改資料分割和角色部署選項  
 您可能必須使用不同於 \<*專案名稱*>.deploymentoptions 檔案中儲存的資料分割和角色選項，來部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 例如，您可能需要保留現有的分割區、角色和角色成員，而非如同 \<*專案名稱*>.deploymentoptions 檔案所示而取代所有現有的分割區、角色和成員。  
  
 若要修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中資料分割和角色的部署，您無法變更專案內的資料分割和角色設定，因為 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 *\<專案名稱>* [屬性頁面] 對話方塊並未顯示這些選項。 如果您要變更角色和資料分割的部署選項，就必須在 \<*專案名稱*>.deploymentoptions 檔案本身內變更此資訊。 下列程序描述如何在 \<*專案名稱*>.deploymentoptions 檔案內變更分割區和角色部署選項。  
  
#### 在已產生輸入檔之後，變更資料分割或角色的部署  
  
-   以互動方式執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並在 [Partition and Role Deployment Options (資料分割和角色部署選項)] 頁面上，指定資料分割和角色的新部署選項。  
  
     – 或 –  
  
-   在命令提示字元下執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 (如需回應檔案模式的詳細資訊，請參閱[執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md))。  
  
     – 或 –  
  
-   以任何文字編輯器開啟 \<*專案名稱*>.deploymentoptions，並手動變更選項。  
  
## 請參閱＜  
 [指定安裝目標](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [指定方案部署的組態設定](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [指定處理選項](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  