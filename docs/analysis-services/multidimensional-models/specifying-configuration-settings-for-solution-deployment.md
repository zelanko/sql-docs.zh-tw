---
title: "指定方案部署的組態設定 | Microsoft Docs"
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
  - "Analysis Services 部署精靈, 組態設定"
  - "輸入檔 [Analysis Services]"
  - "組態選項 [Analysis Services]"
  - "Analysis Services 部署, 組態設定"
  - "部署 [Analysis Services], 組態設定"
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 指定方案部署的組態設定
  [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 會從 \<*專案名稱*>.configsettings 檔案中，讀取資料分割和用於部署指令碼的角色部署選項。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會在下列時機建立此檔案：建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用目前專案的組態設定來建立 \<*專案名稱*>.configsettings 檔案。  
  
## 檢閱部署的組態設定  
 下列是儲存在 \<*專案名稱*>.configsettings 檔案中的組態設定：  
  
-   **資料來源連接字串**：依據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中指定的值，每個資料來源都有連接字串。 在這個檔案中儲存連接字串的其餘部分之前，一定會從字串中移除使用者識別碼和密碼。 不過，如果「部署精靈」直接部署至 Analysis Services 執行個體，您就可以在精靈中加入適當的使用者識別碼和密碼資訊，以便成功處理部署資料庫。 如果「部署精靈」有儲存指令碼，這項連接資訊將不會儲存在部署指令碼本身內。  
  
-   **模擬帳戶**：此設定會指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在每個資料來源中用來執行陳述式的使用者名稱。 如果沒有指定模擬帳戶，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用其登入帳戶來執行陳述式。 如果直接在資料來源中對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登入帳戶授與使用權限，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之所有資料庫中的所有資料庫管理員，都有透過登入帳戶存取資料來源的權限。 如果指定了使用者帳戶和密碼，則在這個檔案中儲存模擬資訊之前，一定會移除這項資訊。 不過，如果「部署精靈」直接部署至 Analysis Services 執行個體，您就可以在精靈中加入適當的使用者識別碼和密碼資訊，以便成功處理部署資料庫。 如果「部署精靈」有儲存指令碼，這項模擬資訊將不會儲存在部署指令碼本身內。  
  
-   **索引鍵錯誤記錄檔**：此設定會指定資料庫中每個 Cube、量值群組、資料分割以及維度之索引鍵錯誤記錄檔的檔案名稱與路徑。  
  
-   **儲存位置**：此設定會指定資料庫中每個 Cube、量值群組以及資料分割的儲存位置。 如果沒有為物件提供任何值，「[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈」就會使用物件的預設位置。 例如，資料分割使用量值群組的位置、量值群組使用 Cube 的位置、而 Cube 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上之物件的預設位置。 此儲存位置可以是本機或通用命名慣例 (UNC) 路徑。  
  
-   **報表伺服器**：此設定會指定資料庫中內，每個 Cube 中定義之每個報表動作的報表伺服器和資料夾位置。  
  
## 修改部署的組態設定  
 在某些情況下，您可能需要使用不同於 \<*專案名稱*>.configsettings 檔案所儲存的組態設定，來部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 例如，您可能需要變更一個或多個資料來源的連接字串，或為特定的資料分割或量值群組指定儲存位置。  
  
 若要在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中修改資料分割與角色的部署，您必須依下述程序變更 \<*專案名稱*>.configsettings 檔案內的這個資訊。 您無法變更專案內的資料分割與角色設定，因為 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 *\<專案名稱>* [屬性頁面] 對話方塊並未顯示這些選項。  
  
> [!NOTE]  
>  組態設定可以套用至所有物件，或僅套用至新建立的物件。 唯有將其他物件部署到先前部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，而且不想要覆寫現有的物件時，才會將組態設定套用至新建立的物件。 若要指定將組態設定套用至所有物件或僅套用至新建立的物件，請在 \<*專案名稱*>.deploymentoptions 檔案中設定此選項。 如需詳細資訊，請參閱[指定資料分割和角色部署選項](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)。  
  
#### 在已產生輸入檔之後，變更組態設定  
  
-   以互動方式執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並在 [組態設定] 頁面上，指定正在部署之物件的組態設定。  
  
     – 或 –  
  
-   在命令提示字元下執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 如需回應檔案模式的詳細資訊，請參閱[執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。  
  
     – 或 –  
  
-   使用任何文字編輯器來修改 \<*專案名稱*>.configsettings 檔案。  
  
## 請參閱＜  
 [指定安裝目標](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [指定資料分割和角色部署選項](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [指定處理選項](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  