---
title: "在 SSMS 中啟用 DirectQuery 模式 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# 在 SSMS 中啟用 DirectQuery 模式
  您可以變更已部署的表格式模型資料存取屬性，藉此啟用 DirectQuery 模式，讓查詢針對後端關聯是資料來源執行，而不是針對位於記憶體內部的快取資料。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，DirectQuery 設定的步驟會因為模型的相容性層級而有所不同。 您可以在下方看到適用於所有相容性層級的步驟。  
  
 本主題假設您已在相容性層級 1200 建立並驗證了記憶體內部表格式模型，且只需要啟用 DirectQuery 存取並更新連接字串。 如果您是從較低的相容性層級開始，則需要先手動升級。 相關步驟請參閱[升級 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)。  
  
> [!IMPORTANT]  
>  建議您使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 而非 Management Studio，來切換資料儲存區模式。 當您使用  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 變更模型，並持續使用到伺服器部署，模型和資料庫就會保持同步。 此外，變更模型中的儲存體模式可讓您檢閱發生的任何驗證錯誤。 如本文所述使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時，則不會回報驗證錯誤。  
  
## 需求  
 在表格式模型中啟用 DirectQuery 模式為多步驟的程序：  
  
-   確認模型沒有可能在 DirectQuery 模式中造成錯誤的功能，然後將模型上的資料儲存區模式從記憶體內部變更為 DirectQuery。  
  
     [DirectQuery 模式 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md) 記載了功能限制清單。  
  
-   檢閱連接字串和已部署資料庫使用的認證，以從後端外部資料庫擷取資料。 請確認連線只有一個，而且其設定適用於查詢執行。  
  
     未專為 DirectQuery 設計的表格式資料庫可能會有多個連線，而現在必須為了 DirectQuery 模式的需求減至一個。  
  
     原先用於處理資料的認證，現在將用以查詢資料。 檢閱 DirectQuery 組態中的帳戶，如果您對作業使用不同的專屬帳戶，則可能需要加以變更。  
  
     DirectQuery 模式是 Analysis Services 在其中信任委派的唯一案例。 如果您的解決方案需要委派以取得使用者特定的查詢結果，用以連接到後端資料庫的帳戶就必須能夠委派發出要求的使用者身分識別，使用者身分識別則必須要有後端資料庫的讀取權限。  
  
-   在最後一個步驟，確認 DirectQuery 模式是透過查詢執行來操作。  
  
## 步驟 1：檢查相容性層級  
 定義資料存取的屬性會在相容性層級間有所不同。 第一步是進行檢查，了解資料庫未於哪個相容性層級。  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，連接到具有表格式模型的執行個體。  
  
2.  在物件總管中，以滑鼠右鍵按一下資料庫 > [屬性] > [相容性層級]。  
  
     值會是 **SQL Server 2016 (1200)** 或 **SQL Server 2012 SP1 或更新版本 (1103)** 等較舊層級。 在下一個步驟中，請遵循適用於該相容性層級的指示。  
  
 當您將表格式模型變更為 DirectQuery 模式時，新的資料儲存區模式會立即生效。  
  
## 步驟 2a：將表格式 1200 資料庫切換成 DirectQuery 模式  
  
1.  在物件總管中，以滑鼠右鍵按一下資料庫 > [屬性] > [模型] > [預設模式]。  
  
2.  將模式設為 [DirectQuery] 。  
  
    |||  
    |-|-|  
    |**有效的值**|**說明**|  
    |**DirectQuery**|查詢會使用為模型定義的資料來源連線，針對後端關聯式資料庫執行。<br /><br /> 模型的查詢會轉換成原生資料庫查詢，並重新導向到資料來源。<br /><br /> 當您處理設為 DirectQuery 模式的模型時，只會編譯及部署中繼資料。 資料本身在模型外部，位於運作中資料來源的資料庫檔案中。|  
    |**匯入**|查詢會以 MDX 或 DAX 針對表格式資料庫執行。<br /><br /> 當您處理設為匯入模式的模型時，會從後端資料來源擷取資料，並將其儲存在磁碟上。 資料庫載入時，資料會完整複製到記憶體中，讓資料表掃描或查詢的速度能夠很快。<br /><br /> 這是表格式模型的預設模式，也是特定 (非關聯式) 資料來源的唯一模式。|  
  
## 步驟 2b：將表格式 1100-1103 資料庫切換成 DirectQuery 模式  
  
1.  在物件總管中，以滑鼠右鍵按一下資料庫 > [屬性] > [資料庫] > [DirectQuery 模式]。  
  
2.  將模式設為 [DirectQuery] 。  
  
     [預設模式] 屬性包含下列項目：  
  
    |||  
    |-|-|  
    |**有效的值**|**說明**|  
    |**InMemory**|查詢只會使用快取的記憶體內部資料。|  
    |**InMemorywithDirectQuery**|查詢預設使用快取，除非在用戶端的連接字串中指定其他項目。<br /><br /> 這是混合模式，其中將分割區個別設定為使用記憶體內部或 DirectQuery。|  
    |**DirectQuery**|查詢只使用關聯式資料來源。|  
    |**DirectQuerywithInMemory**|查詢預設使用關聯式資料來源，除非在用戶端的連接字串中指定其他項目。<br /><br /> 這是混合模式，其中將分割區個別設定為使用記憶體內部或 DirectQuery。|  
  
 **混合式資料儲存區**  
  
 合併使用記憶體內部和以磁碟為基礎的存取時，仍有提供快取，也可用於查詢。 混合模式為您提供許多選項：  
  
-   在快取和關聯式資料來源都可用時，您可以設定慣用連接方法，但最終還是由用戶端控制所使用的資料來源 (利用 DirectQueryMode 連接字串屬性)。  
  
-   您可以在快取上設定資料分割區，如此便永遠不會處理用於 DirectQuery 模式的主要分割區，並且主要分割區必須永遠參考關聯式來源。 有許多方法可以使用資料分割來最佳化模型設計和報表體驗。 如需詳細資訊，請參閱[在 DirectQuery 模式中定義分割區 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)。  
  
-   部署模型之後，您可以變更慣用連接方法。 例如，您可以使用混合模式來進行測試，並且只在全面測試了使用該模型的所有報表或查詢後，才將模型切換到 **[僅限 DirectQuery]** 模式。 如需詳細資訊，請參閱[設定或變更 DirectQuery 的慣用連接方法](../Topic/Set%20or%20Change%20the%20Preferred%20Connection%20Method%20for%20DirectQuery.md)。  
  
## 步驟 3：檢查資料庫的連線屬性  
 切換到 DirectQuery 可能會變更連線的安全性內容，而這取決於資料來源連線的設定方式。 當您變更資料存取模式時，請檢閱模擬和連接字串屬性，以驗證登入對於後端資料庫的持續連線有效。  
  
 如需 DirectQuery 案例的使用者身分識別委派相關背景資訊，請檢閱 **Configure Analysis Services for Kerberos constrained delegation** 中的 [設定 Analysis Services 進行受信任委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 一節。  
  
1.  在物件總管中展開 [連線]，然後按兩下連線以檢視其屬性。  
  
     對於 DirectQuery 模型，必須只為資料庫定義了一個連線，而且資料來源必須為關聯式，並屬於支援的資料庫類型。 請參閱[支援的資料來源 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)。  
  
2.  **連接字串** 應指定伺服器、資料庫名稱，以及 DirectQuery 作業中使用的驗證方法。 如果您使用 SQL Server 驗證，就可以在此處指令資料庫登入。  
  
3.  **模擬資訊** 使用於 Windows 驗證。 對 DirectQuery 模式的表格式模型而言，有效選項包括：  
  
    -   **使用服務帳戶**。 如果 Analysis Services 服務帳戶具有關聯式資料庫的讀取權限，您就可以選擇此選項。  
  
    -   **使用特定的使用者名稱和密碼**。 請指定具有關聯式資料庫讀取權限的 Windows 使用者帳戶。  
  
 請注意，這些認證只用於回應對關聯式資料存放區的查詢；它們不同於處理混合模型快取所用的認證。  
  
 當模型只用於記憶體中時，不能使用模擬。 **ImpersonateCurrentUser**設定無效，除非模型正在使用 DirectQuery 模式。  
  
## 步驟 4︰驗證 DirectQuery 存取  
  
1.  在連接到 SQL Server 關聯式資料庫的情況下，在 Management Studio 中使用 SQL Server Profiler 或 xEvents 開始追蹤。  
  
     如果您使用 Oracle 或 Teradata，請使用該資料庫平台適用的追蹤工具。  
  
2.  在 Management Studio 中，輸入然後執行簡單的 MDX 查詢，例如 `select <some measure> on 0 from model.`。  
  
3.  您應該會在追蹤中看到在關聯式資料庫上執行查詢的證據。  
  
## 請參閱＜  
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [支援的資料來源 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [監視 Analysis Services 執行個體](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  