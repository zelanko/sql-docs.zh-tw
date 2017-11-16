---
title: "Cube、 分割區和維度處理的錯誤組態 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.cubeproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.partitionproperties.errorconfiguration.f1
- sql13.asvs.sqlserverstudio.dimensionproperties.errorconfiguration.f1
ms.assetid: 3f442645-790d-4dc8-b60a-709c98022aae
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 83259b46fd10b45e25e032dfdb692fd654c67260
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="error-configuration-for-cube-partition-and-dimension-processing"></a>Cube、 分割區和維度處理的錯誤組態
  Cube、資料分割或維度物件的錯誤組態屬性決定了在處理期間發生資料完整性錯誤時，伺服器的回應方式。 索引鍵重複、遺漏索引鍵和索引鍵資料行有 Null 值通常會觸發這類錯誤，而造成錯誤的記錄並不會加入至資料庫，您便可設定屬性以決定接下來將發生什麼情況。 依預設，處理作業會停止。 不過，在開發 Cube 期間，您可能希望錯誤發生時仍繼續進行處理，好讓您能夠使用匯入的資料測試 Cube 行為，就算未完全匯入也無妨。  
  
 本主題包含下列各節：  
  
-   [執行順序](#bkmk_exec)  
  
-   [預設行為](#bkmk_default)  
  
-   [錯誤組態屬性](#bkmk_props)  
  
-   [在何處設定錯誤組態屬性](#bkmk_tools)  
  
-   [遺漏索引鍵 (KeyNotFound)](#bkmk_missing)  
  
-   [事實資料表中的 Null 外部索引鍵 (KeyNotFound)](#bkmk_nullfact)  
  
-   [維度中的 Null 索引鍵](#bkmk_nulldim)  
  
-   [造成關聯性不一致的索引鍵重複狀況 (KeyDuplicate)](#bkmk_dupe)  
  
-   [變更錯誤限制或錯誤限制動作](#bkmk_limit)  
  
-   [設定錯誤記錄檔路徑](#bkmk_log)  
  
-   [下一步](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> 執行順序  
 伺服器一律會先執行每筆記錄的 **NullProcessing** 規則再執行 **ErrorConfiguration** 規則。 請務必了解這點，因為當索引鍵資料行中有兩筆以上的錯誤記錄為零時，Null 處理屬性若將 Null 轉換成零可能會接續引起索引鍵重複錯誤。  
  
##  <a name="bkmk_default"></a> 預設行為  
 依預設，處理作業會在牽連到索引鍵資料行的第一個錯誤發生時停止。 此行為是由將允許的錯誤數目指定為零的錯誤限制所控制，而「停止處理」指示詞則告知伺服器應於達到錯誤限制時停止處理。  
  
 凡是由於 Null 或漏遺值或重複值而觸發錯誤的記錄，都將轉換成未知的成員或遭捨棄。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將不會匯入任何違反資料完整性條件約束的資料。  
  
-   預設會轉換成未知的成員是基於 **ConvertToUnknown** 的 **KeyErrorAction**設定。 資料庫中會將配置為未知成員的記錄隔離，以玆證明曾有問題發生，供您在處理完成之後著手調查。  
  
     未知的成員會排除在查詢工作負載之外，但若 **[UnknownMember]** 設為 **[可見]**，則某些用戶端應用程式將予以顯示。  
  
     如果您想要追蹤已轉換成未知成員的 Null 數目，請修改 **NullKeyConvertedToUnknown** 屬性，以便由記錄檔或在 [處理] 視窗中報告這些錯誤。  
  
-   當您手動將 **KeyErrorAction** 屬性設為 **DiscardRecord**時，即會發生捨棄行為。  
  
 透過錯誤組態屬性，您可以決定伺服器在發生錯誤時的回應方式。 選項包括：立即停止處理、繼續處理但停止記錄，或是繼續處理且繼續記錄錯誤。 預設值會隨錯誤的嚴重性而異。  
  
 錯誤計數將記錄所發生的錯誤數目。 如果您設定了上限，則一旦達到該限制時，伺服器回應方式就會變更。 依預設，伺服器將於達到限制之後停止處理。 預設限制是 0，會導致處理作業在算入計數的第一個錯誤發生時停止。  
  
 具有強烈影響的錯誤 (例如，索引鍵欄位遺漏索引鍵或包含 Null 值) 均應快速予以解決。 依預設，這類錯誤將遵守 **ReportAndContinue** 伺服器行為，也就是伺服器會攔截錯誤、將其加入至錯誤計數，然後繼續處理 (除非錯誤限制為零，以致處理作業立即停止)。  
  
 其他錯誤則由於未必會造成資料完整性問題，預設將只會產生錯誤，而並未算入計數或記錄下來 (此為 **IgnoreError** 設定)。  
  
 錯誤計數受到 Null 處理設定的影響。 若是維度屬性，Null 處理選項將決定伺服器在遇到 Null 值時的回應方式。 依預設，數值資料行中的 Null 會轉換成零，而字串資料行中的 Null 將視為空白字串處理。 您可藉由覆寫 **NullProcessing** 屬性及早攔截 Null 值，以免其轉變為 **KeyNotFound** 或 **KeyDuplicate** 錯誤。 如需詳細資訊，請參閱＜ [維度中的 Null 索引鍵](#bkmk_nulldim) ＞。  
  
 錯誤會記錄於 [處理] 對話方塊中，但是並未儲存。 您可以指定索引鍵錯誤記錄檔名稱，將錯誤收集到文字檔。  
  
##  <a name="bkmk_props"></a> 錯誤組態屬性  
 錯誤組態屬性總共有九個。 其中五個用於決定伺服器在發生特定錯誤時的回應方式。 另外四個則是屬於錯誤組態工作負載的範疇，例如允許的錯誤數目、達到限制時要執行的動作、是否將錯誤收集到記錄檔等。  
  
 **伺服器對特定錯誤的回應方式**  
  
|屬性|預設值|其他值|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> 初始化錯誤組態時發生。|**IgnoreError** 既不會記錄錯誤，也未將錯誤算入計數，而只要錯誤計數低於上限，處理作業便會繼續。|**ReportAndContinue** 會記錄錯誤並將其算入計數。<br /><br /> **ReportAndStop** 會報告錯誤並立即停止處理，而無視於錯誤限制。|  
|**KeyNotFound**<br /><br /> 事實資料表中的外部索引鍵在相關維度資料表中沒有相符的主索引鍵時發生 (例如，[銷售額] 事實資料表有一筆記錄，其產品識別碼不存在於 [產品] 維度資料表中)。 在資料分割處理或是雪花維度的維度處理期間，可能會發生此錯誤。|**ReportAndContinue** 會記錄錯誤並將其算入計數。|**ReportAndStop** 會報告錯誤並立即停止處理，而無視於錯誤限制。<br /><br /> **IgnoreError** 既不會記錄錯誤，也未將錯誤算入計數，而只要錯誤計數低於上限，處理作業便會繼續。 觸發此錯誤的記錄預設會轉換成未知的成員，但是您可以變更 **KeyErrorAction** 屬性改為捨棄這些記錄。|  
|**KeyDuplicate**<br /><br /> 在維度中發現重複的屬性索引鍵時發生。 大多數情況下，具有重複的屬性索引鍵是可接受的，但此錯誤將讓您得知發生重複現象，從而可檢查維度的設計是否有缺陷而可能導致屬性之間的關聯性不一致。|**IgnoreError** 既不會記錄錯誤，也未將錯誤算入計數，而只要錯誤計數低於上限，處理作業便會繼續。|**ReportAndContinue** 會記錄錯誤並將其算入計數。<br /><br /> **ReportAndStop** 會報告錯誤並立即停止處理，而無視於錯誤限制。|  
|**NullKeyNotAllowed**<br /><br /> 針對維度屬性設定 **NullProcessing** = Error，或者用以唯一識別成員的屬性索引鍵資料行中存在 Null 值時發生。|**ReportAndContinue** 會記錄錯誤並將其算入計數。|**ReportAndStop** 會報告錯誤並立即停止處理，而無視於錯誤限制。<br /><br /> **IgnoreError** 既不會記錄錯誤，也未將錯誤算入計數，而只要錯誤計數低於上限，處理作業便會繼續。 觸發此錯誤的記錄預設會轉換成未知的成員，但是您可以設定 **KeyErrorAction** 屬性改為捨棄這些記錄。|  
|**NullKeyConvertedToUnknown**<br /><br /> Null 值接續轉換成未知的成員時發生。 針對維度屬性設定 **NullProcessing** = **ConvertToUnknown** 將會觸發此錯誤。|**IgnoreError** 既不會記錄錯誤，也未將錯誤算入計數，而只要錯誤計數低於上限，處理作業便會繼續。|如果您認為此錯誤屬於參考性質，請保留預設值。 否則，您可以選擇使用 **ReportAndContinue** 在 [處理] 視窗中報告錯誤並將其算入錯誤限制的錯誤計數。<br /><br /> **ReportAndStop** 會報告錯誤並立即停止處理，而無視於錯誤限制。|  
  
 **一般屬性**  
  
|**屬性**|**值**|  
|------------------|----------------|  
|**KeyErrorAction**|這是伺服器在 **KeyNotFound** 錯誤發生時所採取的動作。 對此錯誤有效的回應方式包括 **ConvertToUnknown** 或 **DiscardRecord**。|  
|**KeyErrorLogFile**|這是副檔名必須為 .log 的使用者定義檔案名稱，位於服務帳戶具有讀寫權限的資料夾內。 此記錄檔只會包含處理期間產生的錯誤。 如果需要更詳細的資訊，請使用飛行記錄器。|  
|**[KeyErrorLimit]**|這是伺服器允許的資料完整性錯誤數上限，達到此上限之後，即無法繼續處理。 值為 -1 表示沒有限制。 預設值為 0，表示在發生第一個錯誤之後停止處理。 您也可以將其設為整數。|  
|**KeyErrorLimitAction**|這是伺服器在索引鍵錯誤數目達到上限時所採取的動作。 若為 **[停止處理]**，處理作業會立即終止。 若為 **[停止記錄]**，處理作業會繼續，但將不再報告錯誤或予以算入計數。|  
  
##  <a name="bkmk_tools"></a> 在何處設定錯誤組態屬性  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中於部署資料庫之後，或是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的模型專案中，使用屬性頁。 這兩個工具所列出的屬性完全相同。 您也可以在 msmdrsrv.ini 檔案中設定錯誤組態屬性，變更伺服器的錯誤組態預設值，或是針對以指令碼作業形式執行的處理作業，在 **Batch** 和 **Process** 命令中進行設定。  
  
 您可以對任何能夠當成獨立作業處理的物件設定錯誤組態。  
  
#### <a name="sql-server-management-studio"></a>Transact-SQL  
  
1.  在物件總管中，以滑鼠右鍵按一下以下任一物件的 [屬性]：維度、Cube 或資料分割。  
  
2.  在 [屬性] 中按一下 **[錯誤組態]**。  
  
#### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
  
1.  在 [方案總管] 中，按兩下任何維度或 Cube。 下方窗格中的 [屬性] 內隨即出現**[ErrorConfiguration]** 。  
  
2.  或者，如果只有單一維度，則在方案總管中以滑鼠右鍵按一下該維度，然後選擇 [處理]，再從 [處理維度] 對話方塊中選擇 [變更設定]。 [維度索引鍵錯誤] 索引標籤上隨即出現錯誤組態選項。  
  
##  <a name="bkmk_missing"></a> 遺漏索引鍵 (KeyNotFound)  
 遺漏索引鍵值的記錄一概無法加入至資料庫，即使忽略錯誤或錯誤限制不設限亦然。  
  
 當事實資料表中的記錄包含外部索引鍵值，但是該外部索引鍵在相關維度資料表中沒有對應的記錄時，伺服器將於資料分割處理期間產生 **KeyNotFound** 錯誤。 在處理相關維度或雪花維度資料表時，若某一維度的記錄所指定的外部索引鍵不存在於相關維度中，可能也會發生此錯誤。  
  
 一旦發生 **KeyNotFound** 錯誤，便會將違規的記錄配置為未知的成員。 此行為是透過 **[索引鍵錯誤動作]**設為 **ConvertToUnknown**來控制，因此您可以檢視配置的記錄做進一步調查。  
  
##  <a name="bkmk_nullfact"></a> 事實資料表中的 Null 外部索引鍵 (KeyNotFound)  
 依預設，事實資料表的外部索引鍵資料行中的 Null 值會轉換成零。 顯然零不是有效的外部索引鍵值，所以系統會記錄 **KeyNotFound** 錯誤並將其計數算入預設為零的錯誤限制。  
  
 為了讓處理作業能夠繼續，您可以先行處理 Null 免得系統進行轉換而檢查出有錯誤。 若要這樣做，請將 **[NullProcessing]** 設為 **[錯誤]**。  
  
#### <a name="set-nullprocessing-property-on-a-measure"></a>針對量值設定 NullProcessing 屬性  
  
1.  在 SQL Server Data Tools 的 [方案總管] 中，按兩下 Cube，在 Cube 設計師中加以開啟。  
  
2.  在 [量值] 窗格中，以滑鼠右鍵按一下量值並選擇 [屬性]。  
  
3.  在 [屬性] 中，展開 **[來源]** 以檢視 **[NullProcessing]** 屬性。 此屬性依預設會設為 **[自動]** ，意指包含數值資料的欄位內凡是 Null 的 OLAP 項目都將轉換成零。  
  
4.  將其值變更為 [錯誤] 以排除任何具有 Null 值的記錄，避免 Null 轉換成數值 (零)。 這項修改讓您可避開與索引鍵資料行中有多筆記錄為零相關的索引鍵重複錯誤，以及避開值為零的外部索引鍵在相關維度資料表中沒有對等的主索引鍵時所造成的 **KeyNotFound** 錯誤。  
  
##  <a name="bkmk_nulldim"></a> 維度中的 Null 索引鍵  
 若要在雪花維度中發現外部索引鍵的值為 Null 時繼續進行處理，請針對維度屬性的 **NullProcessing** 設定 **KeyColumn** 以先行處理 Null 值。 如此將會捨棄或轉換記錄，避免可能發生 **KeyNotFound** 錯誤。  
  
 處理維度屬性的 Null 情況有兩種選項可用：  
  
-   設定 **NullProcessing**=**UnknownMember** 將具有 Null 值的記錄配置為未知的成員。 這將產生 **NullKeyConvertedToUnknown** 錯誤，而依預設會忽略此錯誤。  
  
-   設定 **NullProcessing**=**Error** 以排除具有 Null 值的記錄。 這將產生 **NullKeyNotAllowed** 錯誤，而此錯誤會記錄下來且其計數將算入索引鍵錯誤限制。 您可以藉著將 **[不允許 Null 索引鍵]** 的錯誤組態屬性設為 **IgnoreError** ，讓處理作業能夠繼續。  
  
 Null 可能會對非索引鍵欄位構成問題，因為 MDX 查詢將視 Null 會解譯為零或空白而傳回不同的結果。 基於這個原因， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供 Null 處理選項讓您可預先定義所需的轉換行為。 如需詳細資訊，請參閱＜ [定義未知的成員和 Null 處理屬性](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) 和 <xref:Microsoft.AnalysisServices.NullProcessing> ＞。  
  
#### <a name="set-nullprocessing-property-on-a-dimension-attribute"></a>針對維度屬性設定 NullProcessing 屬性  
  
1.  在 SQL Server Data Tools 的 [方案總管] 中，按兩下維度，在維度設計師中加以開啟。  
  
2.  在 [屬性] 窗格中，以滑鼠右鍵按一下屬性 (attribute) 並選擇 [屬性]。  
  
3.  在 [屬性] 中，展開 **[KeyColumns]** 以檢視 **[NullProcessing]** 屬性。 此屬性依預設會設為 **[自動]** ，意指包含數值資料的欄位內凡是 Null 的項目都將轉換成零。 將其值變更為 **[錯誤]** 或 **[UnknownMember]**。  
  
     這項修改會導致捨棄或轉換記錄，從而移除觸發 **KeyNotFound** 的基礎條件，以免檢查出有錯誤。  
  
     視錯誤組態而定，此等動作可能會造成將由系統報告和計數的錯誤。 您也許還需要調整其他屬性，例如將 **KeyNotFound** 設為 **ReportAndContinue** 或將 **KeyErrorLimit** 設為非零值，以便系統報告這些錯誤並予算入計數時讓處理作業能繼續進行。  
  
##  <a name="bkmk_dupe"></a> 造成關聯性不一致的索引鍵重複狀況 (KeyDuplicate)  
 依預設，出現索引鍵重複狀況並不會停止處理作業，而是將忽略錯誤且資料庫會排除重複的記錄。  
  
 若要變更此行為，請將 **KeyDuplicate** 設為 **ReportAndContinue** 或 **ReportAndStop** 以報告錯誤。 接著，您可以藉由檢查錯誤，判斷維度的設計是否可能有缺陷。  
  
##  <a name="bkmk_limit"></a> 變更錯誤限制或錯誤限制動作  
 您可以藉著提高錯誤限制，允許處理期間發生更多次錯誤。 提高錯誤限制並無任何方針指引可循，適當的值會因您的實際狀況而不同。 錯誤限制在 **[KeyErrorLimit]** 中是指定成 **[ErrorConfiguration]** properties 中是指定成 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]，而在 **中是指定成維度、Cube 或量值群組屬性 [錯誤組態] 索引標籤上的** 中是指定成 the Error Configuration tab for properties of dimensions, cubes, or measure groups 中是指定成 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 您可以指定一旦達到錯誤限制時，要停止處理還是停止記錄。 例如，假設您設定錯誤限制為 100 且對應的動作是 **StopLogging** 。 若發生第 101 個錯誤，處理作業仍會繼續，但將不再記錄錯誤或予以算入計數。 錯誤限制在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的 **ErrorConfiguration** 屬性中是指定成 **KeyErrorLimitAction**，而在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中維度、Cube 或量值群組屬性 [錯誤組態] 索引標籤中是指定成 [發生錯誤時的動作]。  
  
##  <a name="bkmk_log"></a> 設定錯誤記錄檔路徑  
 您可以指定檔案用來儲存處理期間所報告的索引鍵相關錯誤訊息。 依預設，在 [處理] 視窗的互動式處理期間，錯誤將維持可見，而當您關閉該視窗或工作階段後，錯誤即會遭捨棄。 記錄檔只包含與索引鍵相關的錯誤資訊，和您在處理對話方塊中所見報告的錯誤相同。  
  
 錯誤會記錄到文字檔，其副檔名必須為 .log。 除非發生錯誤，該檔案都將是空的。 依預設，檔案是建立在 DATA 資料夾內。 您可以指定另一個資料夾，前提是 Analysis Services 服務帳戶必須能夠寫入該位置。  
  
##  <a name="bkmk_next"></a> 下一步  
 決定錯誤將會致使停止處理，或是逕行忽略錯誤。 請記住，忽略的只限於錯誤本身。 系統不會忽略造成錯誤的記錄，而是將記錄捨棄或轉換成未知的成員。 違反資料完整性規則的記錄絕不會加入至資料庫。 依預設，處理作業會在第一個錯誤發生時停止，但您可以藉著提高錯誤限制變更此行為。 在開發 Cube 期間，放寬錯誤組態規則以使處理作業能夠繼續，好讓您有資料可進行測試是很實用的作法。  
  
 決定是否要變更預設的 Null 處理行為。 依預設，字串資料行中的 Null 會視為空白值處理，而數值資料行中的 Null 將視為零處理。 如需有關針對屬性 (Attribute) 設定 Null 處理的指示，請參閱＜ [定義未知的成員和 Null 處理屬性](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) ＞。  
  
## <a name="see-also"></a>請參閱＜  
 [記錄屬性](../../analysis-services/server-properties/log-properties.md)   
 [定義未知的成員和 Null 處理屬性](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
  

