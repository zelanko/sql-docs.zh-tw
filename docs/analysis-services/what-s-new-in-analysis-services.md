---
title: "什麼 &#39; s New in Analysis Services |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: 97
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 212fbb3618bbccc58ea077d59f15dca3c31ca71f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-analysis-services"></a>什麼 &#39; s New in Analysis Services
SQL Server 2016 Analysis Services 包含許多新的增強功能提供更佳的效能、 更容易撰寫的方案、 自動化的資料庫管理，增強的關聯性具有雙向交叉篩選，平行資料分割處理和執行更多。 此版本中的大多數增強功能的核心是針對表格式模型資料庫新增的相容性層級 1200。     

## <a name="azure-analysis-services"></a>Azure Analysis Services
2016 SQL PASS 會議中宣告 Analysis Services 現為雲端 Azure 服務。 **Azure Analysis Services**支援在 1200年或更高的相容性層級的表格式模型。 DirectQuery、資料分割、資料列層級安全性、雙向關聯性和翻譯全都支援。 如需深入了解並免費試用，請參閱 [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/)。 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>SQL Server 2016 Service Pack 1 (SP1) Analysis Services 的新功能

[下載 SQL Server 2016 SP1](http://www.microsoft.com/download/details.aspx?id=54276) 

SQL Server 2016 Service SP1 Analysis Services 透過非統一記憶體存取 (NUMA) 感知來提升效能和延展性，並根據 **Intel Threading Building Blocks** (Intel TBB) 來提供最佳化的記憶體配置。 這項新功能藉由在數量更少但更強大的企業伺服器上支援更多使用者，來協助降低擁有權總成本 (TCO)。 

具體而言，SQL Server 2016 SP1 Analysis Services 在下列主要領域做了改進：

-   **NUMA 感知** - 為了改進 NUMA 支援，Analysis Services 內部的記憶體內 (VertiPaq) 引擎現在可以在每個 NUMA 節點上維護個別工作佇列。 如此可確保區段掃描工作會在為區段資料配置記憶體的相同節點上執行。 請注意，預設只會在至少有四個 NUMA 節點的系統上啟用 NUMA 感知。 在兩個節點的系統上，存取遠端配置記憶體的成本通常不需要管理 NUMA 細節的額外負荷。
-   **記憶體配置** - Analysis Services 已透過 Intel Threading Building Blocks 加速，此可調式配置器會為每個核心提供不同的記憶體集區。 當核心數目增加時，系統幾乎能夠以線性方式調整。
-   **堆積片段** - Intel TBB 型可調式配置器也有助於減輕因 Windows 堆積中已出現之堆積片段所造成的效能問題。

效能及延展性測試已顯示在大型多重節點企業伺服器上執行 SQL Server 2016 SP1 Analysis Services 時，查詢輸送量會大幅提升。


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>SQL Server 2016 Analysis Services 中最新消息

雖然此版本中的大多數增強功能是表格式模型特定的增強功能，但是對於多維度模型也已進行了一些改進；例如，DB2 和 Oracle 等資料來源的相異計數 ROLAP 最佳化、使用 Excel 2016 的鑽研複選支援，以及 Excel 查詢最佳化。    

#### <a name="get-the-latest-tools"></a>取得最新的工具
若要充分利用所有的增強功能，在此版本中，務必安裝最新版的 SSDT 和 SSMS。    
- [下載 SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [下載 SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)   

如果您有自訂的 AMO 相依應用程式，您可能需要安裝更新後的 AMO 版本。 如需指示，請參閱[安裝 Analysis Services 資料提供者 &#40;AMO、ADOMD.NET、MSOLAP&#41;](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)。    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>TechNet 虛擬實驗室︰SQL Server 2016 Analysis Services
想要實機操作以深入了解嗎？ 請遵循 [SQL Server 2016 Analysis Services 虛擬實驗室的新功能](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true)中的逐步指示。
在此實驗室中，您將建立及監視擴充事件 (xEvent)、將表格式專案升級至相容性層級 1200、使用 Visual Studio 組態、實作新的計算功能、實作新的資料表關聯性功能、設定顯示資料夾、管理模型轉換、使用新的表格式模型指令碼語言 (TMSL)、使用 PowerShell，以及試用新的 DirectQuery 模式功能。

## <a name="modeling"></a>模型化    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>提升表格式 1200 模型的模型化效能    
若為表格式 1200 模型，SSDT 中的中繼資料作業速度會比表格式 1100 或 1103 模型快很多。 經由比較，在相同的硬體上，在設為 SQL Server 2014 相容性層級 (1103) 的模型上建立 23 個資料表的關聯性需要 3 秒，而在設為相容性層級 1200 的模型上建立相同的關聯性則不到一秒。    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>SSDT 中表格式 1200 模型新增的專案範本    
在此版本中，您不再需要兩個版本的 SSDT 來建置關聯式和 BI 專案。 [SQL Server Data Tools for Visual Studio 2015](http://msdn.microsoft.com/library/mt204009.aspx) 新增 Analysis Services 解決方案的專案範本，包括用來在 1200 相容性層級建置模型的 **Analysis Services 表格式專案** 。 多維度和資料採礦解決方案的其他 Analysis Services 專案範本也包含在內，但與先前的版本位於相同的功能層級 (1100 或 1103)。    
### <a name="display-folders"></a>顯示資料夾
表格式 1200 模型現在提供顯示資料夾。 顯示資料夾定義於 SQL Server Data Tools 並呈現在用戶端應用程式 (如 Excel 或 Power BI Desktop) 中，有助於將大量的量值組織成個別的資料夾，並新增一個視覺階層，以便在欄位清單中瀏覽。
### <a name="bi-directional-cross-filtering"></a>雙向交叉篩選
此版本中有內建的新方法可以啟用表格式模型中的雙向交叉篩選，因此不需要透過自訂 DAX 因應措施在資料表關聯性之間散佈篩選內容。 可以建立高度確定的方向時，才會自動產生篩選。 如果資料表關聯性之間有多個查詢路徑的形式模糊不清，將不會自動建立篩選。 如需詳細資訊，請參閱 [SQL Server 2016 Analysis Services 中適用於表格式模型的雙向交叉篩選](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 。
 ### <a name="translations"></a>翻譯    
 您現在可以在表格式 1200 模型中儲存已翻譯的中繼資料。 模型中的中繼資料包含 **Culture**、已轉譯標題和已轉譯描述的欄位。 若要新增翻譯，請使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [模型] > [翻譯] 命令。 如需詳細資訊，請參閱[表格式模型中的翻譯 &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)。    
 ### <a name="pasted-tables"></a>貼上的資料表    
 您現在可以在模型包含貼上的資料表時，將 1100 或 1103 表格式模型升級為 1200。 建議使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]。 在 SSDT 中，將 **CompatibilityLevel** 設定為 1200，然後部署到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體。 如需詳細資訊，請參閱 [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) 。    
 ### <a name="calculated-tables-in-ssdt"></a>SSDT 中的導出資料表    
「導出資料表」  是以 SSDT 中的 DAX 運算式或查詢為基礎的僅限模型建構。 部署於資料庫時，無法區別計算資料表與一般資料表。    

 計算資料表有數個用途，包括建立新的資料表，以特定角色公開現有的資料表。 典型的範例是在多個內容 (訂單日期、出貨日期等) 中運作的日期資料表。 藉由建立特定角色的計算資料表，您現在可以啟動資料表關聯性，以使用計算資料表來促進查詢或資料互動。 計算資料表的另一個用途是將現有資料表的各部分合併成只存在於模型中的全新資料表。  如需詳細資訊，請參閱[建立導出資料表 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md)。    
 ### <a name="formula-fixup"></a>公式修復    
 利用表格式 1200 模型的公式修復，SSDT 會自動更新目前參考已重新命名的資料行或資料表的所有量值。    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Visual Studio 組態管理員支援    
 為了支援多個環境 (例如測試和生產前環境)，Visual Studio 允許開發人員使用組態管理員建立多個專案組態。 多維度模型已經運用這項功能，但表格式模型則未運用。 在此版本中，您現在可以使用組態管理員來部署到不同的伺服器。    

## <a name="instance-management"></a>執行個體管理    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>管理 SSMS 中的表格式 1200 模型    
 在此版本中，表格式伺服器模式中的 Analysis Services 執行個體可以執行任何相容性層級 (1100、1103、1200) 的表格式模型。 最新版的 [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) 已更新，可以顯示屬性並提供 1200 相容性層級之表格式模型的資料庫模型管理。    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>平行處理表格式模型中的多個資料表資料分割    
 此版本為具有兩個或多個資料分割的資料表提供新的平行處理功能，以提高處理效能。 此功能沒有任何組態設定。 如需設定資料分割和處理資料表的詳細資訊，請參閱[表格式模型資料分割 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)。    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>在 SSMS 中將電腦帳戶新增為系統管理員    
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 系統管理員現在可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 將電腦帳戶設定為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Administrators 群組的成員。 在 [選取使用者或群組]  對話方塊中，設定電腦網域的 [位置]  ，然後新增 [電腦]  物件類型。 如需詳細資訊，請參閱 [將伺服器系統管理員權限授與 Analysis Services 執行個體](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。    
 ### <a name="dbcc-for-analysis-services"></a>DBCC for Analysis Services    
 Database Consistency Checker (DBCC) 會在內部執行，以偵測資料庫負載的潛在資料損毀問題，但如果您懷疑您的資料或模型有問題，也可以視需要執行。 DBCC 會依據模型為表格式或多維度模型而執行不同的檢查。 如需詳細資訊，請參閱 [Database Consistency Checker &#40;DBCC&#41; for Analysis Services 表格式和多維度資料庫](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)。    
 ### <a name="extended-events-updates"></a>擴充事件更新    
 此版本新增圖形化使用者介面至 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，以設定及管理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 擴充事件。 您可以設定即時資料流來即時監視伺服器活動、讓工作階段資料載入記憶體中以便快速分析，或將資料流儲存至檔案以便進行離線分析。 如需詳細資訊，請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 和 [Using extended events with Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx)(使用擴充事件搭配 Analysis Services) (Guy in a Cube 部落格文章和影片)。    



## <a name="scripting"></a>指令碼
 ### <a name="powershell-for-tabular-models"></a>表格式模型的 PowerShell    
 此版本包含相容性層級 1200 之表格式模型的 PowerShell 增強功能。 您可以使用所有適用的 Cmdlet，再加上表格式模式特定的 Cmdlet︰ [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) 和 [Invoke-ProcessTable Cmdlet](../analysis-services/powershell/invoke-processtable-cmdlet.md)。    
 ### <a name="ssms-scripting-database-operations"></a>SSMS 指令碼資料庫作業    
 在 [最新版的 SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)中，現已針對資料庫命令啟用指令碼，包括 Create、Alter、Delete、Backup、Restore、Attach、Detach。 輸出是 JSON 格式的表格式模型指令碼語言 (TMSL)。 如需詳細資訊，請參閱[表格式模型指令碼語言 &#40;TMSL&#41; 參考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)。    
 ### <a name="analysis-services-execute-ddl-task"></a>Analysis Services 執行 DDL 工作    
 [Analysis Services 執行 DDL 工作](../integration-services/control-flow/analysis-services-execute-ddl-task.md) 現在也接受表格式模型指令碼語言 (TMSL) 命令。     
 ### <a name="ssas-powershell-cmdlet"></a>SSAS PowerShell Cmdlet    
 SSAS PowerShell Cmdlet **Invoke-ASCmd** 現在接受表格式模型指令碼語言 (TMSL) 命令。 未來版本中可能會更新其他 SSAS PowerShell Cmdlet，以便使用新的表格式中繼資料 (版本資訊中將詳列例外狀況)。    
如需詳細資訊，請參閱 [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) 。    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>SSMS 中支援的表格式模型指令碼語言 (TMSL)    
  您現在可以使用 [最新版的 SSMS](http://msdn.microsoft.com/library/mt238290.aspx)來建立指令碼，將表格式 1200 模型的大部分管理工作自動化。 目前可以編寫下列工作的指令碼︰任何層級的 Process，以及資料庫層級的 CREATE、ALTER、DELETE。    
    
 在功能上，TMSL 相當於可提供多維度物件定義的 XMLA ASSL 延伸模組，不同之處在於 TMSL 會使用 **model**、 **table**和 **relationship** 等原生描述元來描述表格式中繼資料。 如需結構描述的詳細資訊，請參閱[表格式模型指令碼語言 &#40;TMSL&#41; 參考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)。    
    
 針對表格式模型產生的 JSON 型指令碼可能如下所示︰    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

裝載是一份 JSON 文件，該文件可以如上述範例一樣精簡，或使用一組完整物件定義高度裝飾。 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)描述語法。

在資料庫層級，CREATE、ALTER 和 DELETE 命令會在熟悉的 XMLA 視窗中輸出 TMSL 指令碼。  其他命令 (例如 Process) 也可以在此版本中建立指令碼。 未來版本中可能新增許多其他動作的指令碼支援。    

**可編寫指令碼的命令** | **描述**
--------------- | ----------------
建立|新增資料庫、連線或分割區。 ASSL 對等項目為 CREATE。
createOrReplace|藉由覆寫先前的版本來更新現有的物件定義 (資料庫、連線或分割區)。 ASSL 對等項目為 ALTER，其 AllowOverwrite 設定為 true 且 ObjectDefinition 設定為 ExpandFull。
刪除|移除物件定義。 ASSL 對等項目為 DELETE。
refresh|處理物件。 ASSL 對等項目為 PROCESS。

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>改良的 DAX 公式編輯
公式列更新使用語法顏色設定來區分函數、欄位和量值，協助您更輕鬆地撰寫公式，而語法顏色設定會提供智慧型函數和欄位建議，並使用錯誤「波浪線」 來告訴您 DAX 運算式是否有任何部分錯誤。 它也可讓您使用多行程式碼 (Alt + Enter 鍵) 和縮排 (Tab 鍵)。 公式列現在也可讓您撰寫註解做為您的量值的一部分，只要輸入 “//”，同一行上這些字元之後的一切將會被視為註解。

### <a name="dax-variables"></a>DAX 變數    
此版本現在會在 DAX 中包含變數的支援。 變數現在可以將運算式的結果儲存為具名變數，然後做為引數傳遞至其他量值運算式。 一旦計算變數運算式的結果值，這些值就不會變更，即使另一個運算式中參考的此變數。 如需詳細資訊，請參閱 [VAR 函數](http://msdn.microsoft.com/library/mt243785.aspx)。    
### <a name="new-dax-functions"></a>新的 DAX 函數
在此版本中，DAX 引進了超過&50; 個新函數，以在 Power BI 中支援更快速的計算和增強的視覺效果。 如需詳細資訊，請參閱 [New DAX Functions](http://msdn.microsoft.com/library/mt704075.aspx)(新的 DAX 函數)。
### <a name="save-incomplete-measures"></a>儲存不完整的量值
您現在可以直接在表格式 1200 模型專案中儲存不完整的 DAX 量值，然後在您準備好繼續進行時再次取用。
### <a name="additional-dax-enhancements"></a>其他 DAX 增強功能
- 非空白計算 - 減少非空白所需的掃描數目。
- 量值融合 - 同一個資料表中的多個量值會結合成單一儲存引擎查詢。
- 群組集合 - 當查詢要求多種資料粒度 (總計/年/月) 的量值時，會以最低層級傳送單一查詢，並從此最低層級衍生其餘資料粒度。     
- 多餘聯結刪除 - 對儲存引擎的單一查詢會傳回維度資料行和量值。
- IF/SWITCH 的嚴格評估 - 條件為 false 的分支將不再產生儲存引擎查詢。 之前會積極地評估分支，但之後捨棄結果。     
    
## <a name="developer"></a>開發人員    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>AMO 中表格式 1200 可程式性的 Microsoft.AnalysisServices.Tabular 命名空間
 Analysis Services 管理物件 (AMO) 會進行更新以納入新的表格式命名空間 (可供管理 SQL Server 2016 Analysis Services 的表格式模式執行個體)，以及提供資料定義語言 (可供以程式設計方式建立或修改表格式 1200 模型)。 請瀏覽 [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) 以在 API 上讀取。    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Analysis Services 管理物件 (AMO) 更新
 [Analysis Services 管理物件 &#40;AMO&#41;](http://msdn.microsoft.com/library/mt436122.aspx) 已經重構以包含第二個組件 Microsoft.AnalysisServices.Core.dll。 不論伺服器模式為何，新的組件都會區隔 Analysis Services 中廣泛應用的一般類別 (例如伺服器、資料庫和角色)。    
    
 之前，這些類別是原始 Microsoft.AnalysisServices 組件的一部分。 將這些類別移至新的組件即可為 AMO 的未來擴充做好準備，並清楚劃分一般和特定內容的 API。    
    
 現有的應用程式不受新的組件影響。 不過，假使您因故選擇使用新的 AMO 組件來重新建置應用程式，請務必新增 Microsoft.AnalysisServices.Core 的參考。    
    
 同樣地，載入並呼叫 AMO 的 PowerShell 指令碼現在必須載入 Microsoft.AnalysisServices.Core.dll。 請務必先更新指令碼。  

### <a name="json-editor-for-bim-files"></a>BIM 檔案的 JSON 編輯器
Visual Studio 2015 中的 [程式碼檢視] 現在會針對表格式 1200 模型呈現 JSON 格式的 BIM 檔案。 Visual Studio 的版本可決定是否要透過內建 JSON 編輯器以 JSON 格式呈現 BIM 檔案，或呈現為簡單文字。

若要使用 JSON 編輯器並能夠展開和摺疊模型的區段，您將需要有最新版的 SQL Server Data Tools 和 Visual Studio 2015 (任何版本，包括免費的 Community Edition)。 對於所有其他版本的 SSDT 或 Visual Studio，BIM 檔案會以 JSON 呈現為簡單文字。
空的模型至少包含下列 JSON：

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> 請避免直接編輯 JSON。 這麼做可能會損毀模型。    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>MS-CSDLBI 2.0 結構描述中的新元素    
 下列元素已新增至 [MS-CSDLBI] 2.0 結構描述中定義的 **TProperty** 複雜類型：    
    
|元素|定義|    
|-------------|----------------|    
|DefaultValue|一個屬性，可指定在評估查詢時使用的值。 DefaultValue 是選擇性屬性，但如果無法彙總成員所提供的值，則會自動選取該屬性。|    
|Statistics|與資料行相關聯的基礎資料中的一組統計值。 這些統計值是由 TPropertyStatistics 複雜類型所定義，而如概念結構定義檔案格式的 2.1.13.5 節與商業智慧註釋文件所述，只有在不耗費許多資源即可產生時才會提供這些統計值。|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>新的 DirectQuery 實作    
此版本已大幅改進表格式 1200 模型的 DirectQuery。 摘要如下：    
-   DirectQuery 現在會產生較簡單的查詢，進而提供較佳的效能。    
-   對於定義模型設計和測試所用的範例資料集，提供額外控制。    
-   DirectQuery 模式中的表格式 1200 模型現在支援資料列層級安全性 (RLS)。 先前，RLS 的存在導致無法在 DirectQuery 模式中部署表格式模型。    
-   DirectQuery 模式中的表格式 1200 模型現在支援導出資料行。 先前，導出資料行的存在導致無法在 DirectQuery 模式中部署表格式模型。    
-   效能最佳化包括 VertiPaq 和 DirectQuery 的多餘聯結刪除。 

### <a name="new-data-sources-for-directquery-mode"></a>DirectQuery 模式的新資料來源    
 現在支援 DirectQuery 模式中表格式 1200年模型的資料來源包括 Oracle、 Teradata 和 Microsoft 分析平台 （之前稱為平行資料倉儲）。    
    
如需詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。    

## <a name="see-also"></a>另請參閱
[Analysis Services 團隊部落格](http://blogs.msdn.microsoft.com/analysisservices/)    
[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)    
     


