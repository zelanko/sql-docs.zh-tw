---
title: "SQL Server Data Tools (SSDT) 的變更記錄 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8798c5319cdce7b68f71868722aacfbf4cb34d9f
ms.lasthandoff: 04/11/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 的變更記錄
此變更記錄適用於 [Visual Studio 2015 的 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx) (與 [SQL Server 2016](https://msdn.microsoft.com/library/ms130214.aspx) 一併發行)。  
  
如需新功能和變更功能的詳細文章，請造訪 [SSDT 團隊部落格](https://blogs.msdn.microsoft.com/ssdt/)。  

## <a name="ssdt-165-for-sql-server-2016"></a>SSDT 16.5 (適用於 SQL Server 2016)
發行日期︰2016 年 10 月 20 日

組建編號：14.0.61021.0

**新功能**


### <a name="connection-improvements"></a>連線功能改進

* 在 [瀏覽]**** 索引標籤中的新搜尋方塊可協助您篩選您的本機伺服器、網路伺服器和 Azure SQL 資料庫。 如果您有大量伺服器或資料庫出現在這些清單中，此功能非常有用。
* [歷程記錄]**** 索引標籤有右鍵功能表選項可釘選/取消釘選 [我的最愛]，還有新選項可從歷程記錄移除連線。

### <a name="sqlpackage-and-dacfx-api-improvements"></a>SqlPackage 和 DacFx API 功能改進

您現在可以使用 SqlPackage.exe 和 DacFx API，只以一個動作就能產生部署報表、部署指令碼，並發行至資料庫。 這對於想要保留部署期間發行內容報表的任何人來說非常節省時間。 另一個好處是在 Azure 的案例中，會針對主要資料庫與部署目標資料庫建立不同的指令碼。 在此之前只會建立單一指令碼，對於重複的部署不是很有用。

針對 SqlPackage 的 Publish 和 Script 動作，加入兩個新的引數。

* DeployScriptPath (簡短名稱︰dsp)。 這是要撰寫部署指令碼的選擇性路徑。 對於 Azure 部署，如果有 TSQL 命令要建立或修改資料庫，將會對主要指令碼寫入相同的路徑，但會使用 “Filename_Master.sql” 做為輸出檔案名稱。
* DeployReportPath (簡短名稱︰drp)。 這是要撰寫部署報表的選擇性路徑。

請注意，Script 動作應使用現有的「輸出路徑」引數或新的指令碼/報表特定引數，但不是同時使用兩者。

範例使用方式︰

**Publish 動作**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**Script 動作**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

DacFx 中已加入兩個新的 API：DacServices.Publish() 和 DacServices.Script()。 這些 API 也支援在單一作業中執行發行 + 編寫指令碼 + 報告的動作。 範例使用方式︰

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services 與 Reporting Services**

使用大型 DAX 運算式時，SSAS 表格式設計工具 DAX 剖析器已經改善效能。
如需詳細資訊，請參閱 [Analysis Services 部落格文章 (英文)](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)。

### <a name="fixed--improved-this-month"></a>本月份修正/改進內容

**資料庫工具**

* [連接錯誤 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – Columns cannot be selected from CROSS APPLY OPENJSON with explicit schema (無法從有明確結構描述的 CROSS APPLY OPENJSON 選取資料行)
* 已修正 - 在自動產生的歷程記錄資料表索引中，DacFx 在重新部署時會卸除索引的問題
* 已修正 - DacFx 批次剖析器未剖析逸出括號 ']' 字元而導致發行失敗的問題
* 已改進 - SqlPackage 現在在說明輸出中會包含每個動作的描述
* 已修正 - 編輯進階選項時，以及編輯「發行」、「結構描述比較」和其他檔案中儲存的連接字串時，沒有保留 [連接] 對話方塊的 [記住密碼] 選項
* 已修正 - 對於在 [歷程記錄] 索引標籤中 IntegratedAuthentication=true 所顯示的連接，連接屬性中的 [驗證] 欄位為空白。 現在這會如預期般顯示「Windows 驗證」
* 已修正 - 沒有保留 [工具] -> [選項] -> [文字編輯器] 下對 SQL Server 工具 Intellisense 設定的變更
* 已改進 - [連接] 對話方塊的 [歷程記錄] 索引標籤中的 [釘選]/[取消釘選] 按鈕現在更緊密，降低捲軸出現的可能性
* 已修正 - 已修正 [連接] 對話方塊中幾個協助工具問題。

**Analysis Services 與 Reporting Services**

* 已修正在某些情況下在 SSDT AS 表格式設計工具中按一下資料格中的捲軸指標會當機的問題
* 已修正沒有選項可將連線模擬為 SSDT AS 表格式中目前使用者的問題
* 已修正在 SSDT AS 表格式設計工具中將公式列展開太遠而無法重新開啟專案的問題
* 已修正在 SSDT AS 表格式設計工具中若已選取資料表索引標籤，按向下鍵可能會發生當機的問題
* 已修正在 SSDT AS 專案中 [在 Excel 中進行分析] 不會連線至下層 AS 伺服器版本的問題

**整合服務**

* 已修正連接錯誤 [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks)︰Move Multiple Integration Service Package Tasks (移動多個整合服務封裝工作)





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4 (適用於 SQL Server 2016)
發行日期︰2016 年 9 月 20 日

組建編號：14.0.60918

**新功能**

SqlPackage.exe 和 Data-Tier Application Framework (DacFx) API 現在支援結構描述比較。 如需詳細資訊，請參閱 [SqlPackage 和 Data-Tier Application Framework 中的結構描述比較 (英文)](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/)。

**Analysis Services - SSDT 表格式 (SSAS) 的整合式工作區模式**

SSDT 表格式現在包含內部的 SSAS 執行個體，若啟用整合式工作區模式，則 SSDT 表格式會自動在背景啟動此執行個體，讓您可以在模型設計師中新增及檢視資料表、資料行和資料，無需提供外部工作區伺服器執行個體。 整合式工作區模式不會變更 SSDT 表格式與工作區伺服器及資料庫搭配運作的方式。 變更之處在於 SSDT 表格式裝載工作區資料庫的位置。 若要啟用整合式工作區模式，請在建立新的表格式專案時顯示的 [表格式模型設計師] 對話方塊中選取 [整合式工作區] 選項。 對於目前使用明確工作區伺服器的現有表格式專案，您可以在於 [方案總管] 中選取 Model.bim 檔案時顯示的 [屬性] 視窗中將 [整合式工作區模式] 參數設定為 True，切換到整合式工作區模式。 如需詳細資訊，請參閱 [Analysis Services 部落格文章 (英文)](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)。

**更新和修正**
**資料庫工具︰**

- [連接問題 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775)︰Temporal tables broken in VS Data Tools July update 14.0.60629.0, "Value cannot be null. Parameter name: reportedElement" (VS 資料工具 7 月更新 14.0.60629.0 中的時態表損毀，「值不可以是 Null。參數名稱：reportedElement」)
- [連接問題 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648)：IsPersistedNullable shows as different in SSDT Comparison (IsPersistedNullable 在 SSDT 比較中顯示為不同)
- [連接問題 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735)︰Identity is reset when importing a BACPAC (匯入 BACPAC 時會重設識別)
- [連接問題 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167)︰Running SSDT unit tests leaves temp files behind (執行 SSDT 單元測試留下暫存檔案)
- [連接問題 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712)︰Backwards compatibility breakage – AppLocal and Nugetization (回溯相容性損毀 - AppLocal 和 Nugetization)

**Analysis Services 與 Reporting Services**

* 已修正在 SSDT 中當編輯 DirectQuery 導出資料行的 DAX 時會出現錯誤提示快顯視窗的問題。
* 已修正在 SSDT AS 表格式方格中當 Windows 縮放比例設定在高 DPI 200%+ 時，KPI 圖示未顯示在量值方格中中的問題。
* 已修正在 SSDT AS 中貼上大型資料表資料可能會讓表格式專案沒有回應的問題。
* 已修正在 SSDT AS 表格式模型編輯器中重新命名連線的易記名稱時，將模型標示為必須儲存變更的問題。
* 已修正在 SSDT AS 表格式專案中 [管理關聯性] 對話方塊中的資料行寬度無法調整大小的問題。
* 已修正在 SSDT AS 表格式 1200 層級的模型中，若地區設定為例如德文，從 Excel 貼上資料沒有正確將逗號視為小數分隔符號的問題。
* 已修正在設定某些 KPI 圖示集的 SSDT AS 專案中可能會產生「無法擷取此視覺物件的資料」錯誤的問題。
* 已修正 SSDT AS 專案屬性對話方塊在高 DPI 縮放比例調整大小時正確錨定的問題。
* 已修正在 SSDT AS 專案中升級內含貼上的資料表的特定模型時可能會造成錯誤的問題。
* 已修正在 SSDT AS 中從 Excel 貼上整個工作表資料列非常緩慢且建立許多不必要資料行的問題。
* 已修正在 SSDT AS 中大型靜態 DataTable 運算式的剖析和反白顯示非常緩慢或似乎停止回應的問題。
* 已修正在 SSDT AS 中將量值和 KPI 值新增至編輯器中目前所選檢視方塊的問題。
* 已修正在 SSDT 中從 SQL Azure 匯入 AS 專案的資料不支援除了 "dbo" 以外之結構描述類型的問題。



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3 (適用於 SQL Server 2016)
發行日期︰2016 年 8 月 15 日

組建編號：14.0.60812.0  

**新功能**

- **發行版本控制與編號︰**發行版本現在以數值標記而不是依月份標記。 這與新的 SSMS 原則一致，並簡化在一個月中有多個版本或 hotfix 時的情況。 此版本是 16.3，表示在 RTM 版本之後的第三個更新。 任何 hotfix 將是 16.3.1，依此類推，下一個更新 (下個月的計劃) 將是 16.4。
- **Analysis Services - 表格式模型總管：**表格式模型總管可讓您在模型中方便瀏覽各種中繼資料物件，例如資料來源、資料表、量值和關聯性。 它會實作為獨立的工具視窗，您可以在 Visual Studio 中開啟 [檢視] 功能表，指向 [其他視窗]，然後按一下 [表格式模型總管] 來顯示。 表格式模型總管預設會出現在方案總管區域的另一個索引標籤上。 表格式模型總管會將中繼資料物件組織在與表格式 1200 模型結構描述十分類似的樹狀結構中，而且有更多新功能。
- **資料庫工具 - Always Encrypted**︰此版本提供新的[Always Encrypted 金鑰管理](https://msdn.microsoft.com/library/mt708953.aspx)對話方塊，可輕鬆地將資料行主要金鑰或資料行加密金鑰加入至資料庫專案或 SQL Server 物件總管中的即時資料庫。 此版本支援 Windows 憑證存放區中的憑證。 未來的版本將會支援 Azure 金鑰保存庫和 CNG 提供者。
    - 在建立資料行主要金鑰或資料行加密金鑰時，您可能會發現按一下 [更新資料庫] 之後，SQL Server 物件總管無法立即反映所做的變更。 若要解決這個問題，請重新整理 SQL Server 物件總管中的資料庫節點。
    - 如果您嘗試加密的資料表資料行含有來自 SQL Server 物件總管的資料，您可能會失敗。 目前只有在 SSDT 資料庫專案和 SSMS 中才支援這項功能。 未來版本中將會支援 SQL Server 物件總管。


**更新和修正**
* **資料庫工具︰**
    - **SSDT：**
        - 連接錯誤 1898001 [已修正資料行描述 128 個字元限制的問題](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters)。
        - 已修正從 VS 發行資料庫並未在發行設定檔 xml 中套用 DatabaseServiceObjective 屬性的問題。
        - 連接錯誤 2900167 [已修正不正確保留暫存檔的單元測試問題](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind)。
        - 已修正 [資料庫設定] 的 [保留週期] 下拉式方塊被截斷的問題。
        - 已修正變更密碼時遺漏在 SQL CLR 專案屬性上驗證空白舊密碼的問題。
    - **DACFx：**
        - 已修正未針對 SqlAzureV12 錯誤更新 DACFx 相容性層級的問題。
        - 已修正不正確地從模型比較排除 IsAutoGeneratedHistoryTable 屬性的問題。

- **Analysis Services 與 Reporting Services**
    - **SSDT：**
        - 已修正伺服器連線中斷時，無法儲存表格式模型的問題。
        - 已修正 SSDT 因為 AS 中可能存在的無限迴圈問題而變成沒有回應的問題。
        - 已修正根據您如何認可運算式而造成不一致行為的 DAX 運算式問題。
        - 已修正建立 KPI 時的 VS 當機問題。
        - 已修正為 SQL Server 2008 R2、2012 和 2014 產生無效報表的問題。
        - 已修正造成 .dwpro 專案無限迴圈錯誤的階層順序問題。
        - 已修正降級 RDL 需要完整重建而造成使用者混淆的 RS RDL 問題。
        - 已修正「在用戶端工具中隱藏」沒有作用的 KPI 問題。
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT 7 月 (適用於 SQL Server 2016)  
發行日期︰2016 年 6 月 30 日  
  
組建編號︰14.0.60629.0  
  
**新功能**  
* **Always Encrypted 支援︰**對於包含 Always Encrypted 資料行的資料庫，此版本透過我們的核心 API 和命令列工具 (SqlPackage.exe) 加入 Always Encrypted 的完整支援。 您可以利用所有完整支援的 Always Encrypted 功能，建置及發行資料庫專案。  
* **時態表增強支援︰**透過在改變之前取消連結時態表，然後在完成之後再重新連結來簡化體驗。 這表示時態表在支援的作業方面有其他資料表類型 (標準、記憶體內部) 的同位。 
* **SqlPackage.exe 和安裝變更︰**從 SQL Server 引擎隔離出 SSDT 的變更以及 SSMS 更新。 如需詳細資訊，請參閱 [SSDT 和 SqlPackage.exe 安裝和更新的變更 (英文)](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/)。

 

**更新和修正**
* **資料庫工具︰**
    * 從現在起，SSDT 將永遠不會停用資料庫的「透明資料加密」(TDE)。 先前因為停用專案資料庫設定中的預設加密選項，所以會關閉加密。 透過此修正可啟用加密，但在發行期間永遠不會停用。 
    * 增加初始連線期間 Azure SQL DB 連線的重試計數和復原能力。
    * 如果預設檔案群組不是 PRIMARY，匯入/發行至 Azure V12 將會失敗。 現在發行時會忽略此設定。
    * 已修正當匯出的資料庫含有啟用「引號識別項」的物件時，匯出驗證可能會在某些情況下失敗的問題。
    * 已修正在建立 Hekaton 資料表時不正確加入 TEXTIMAGE_ON 選項的問題，這是不允許的動作。
    * 已修正匯出在資料階段完成之後因為寫入 model.xml 檔案而花費很長的時間匯出大量資料，造成要重新寫入 .bacpac 檔案內容的問題。
    * 已修正使用者未出現在 Azure SQL DW 和 APS 連線之 [安全性] 資料夾的問題。


 * **Analysis Services 與 Reporting Services：**
    * 已修正 MSOLAP OLEDB 提供者中只安裝 32 位元提供者，影響連線到 SQL Server 2014 的 64 位元 Excel 2016 的 SxS 問題 (未重現在從 Office365 的 ClickOnce 安裝，只重現在 MSI Excel 安裝)。
    * 已修正將含有貼上資料表的 AS 模型從 1103 升級為 1200 相容性層級 (可能產生「關聯性使用無效資料行識別碼」錯誤) 時，要讓極端案例 (corner case) 更健全的問題。
    * 已修正當 SSDT-BI 2013 位於相同電腦上，解除安裝 SSDT 2015 之後可能無法再匯入 AS 模型中資料的 SxS 問題 (墨水匣共用登錄設定)。
    * 已改進當 AS 引擎的連線中斷 (亦即 SSDT 整夜開啟並回收 AS 伺服器，或連線暫時中斷的其他情況) 時解決問題/當機的穩固性。 
    * 已修正在多重監視器案例中，在不同於 VS 的螢幕上開啟對話方塊的問題。 
    * 已修正/啟用在 AS 模型貼上的資料表中從 HTML 資料表 (方格資料) 貼上的支援。 
    * 已修正升級無法將空白的貼上資料表升級為 1200 (只用來做為量值的容器資料表) 的問題。 
    * 已修正將含有貼上資料表的 AS 表格式模型升級為 1200 以使用 CalcTables (用於 1200 中的貼上資料表) 解決 AS 引擎問題，以便在升級之後直接對新的導出資料表執行處理序的問題。 
    * 已修正使用不完整的 DAX 運算式取消建立新的 AS 1200 模型導出資料表可能會當機的問題。 
    * 已修正當資料庫名稱和資料表名稱相同時，從 AS 伺服器將 1200 模型匯入至 SSDT AS 專案的問題。 
    * 已修正在 1103 表格式模型中編輯 KPI 量值的問題。 
    * 已修正在 AS 1200 模型的方格中貼上 KPI 量值時發生物件參考未設定的例外狀況。 
    * 已修正無法從 1200 模型中的圖表檢視刪除導出資料表中資料行的問題。 
    * 已修正在程式碼檢視中檢視 model.bim 專案檔屬性時發生物件參考未設定的例外狀況。 
    * 已修正將資料貼上 AS 模型方格以建立貼上的資料表會使用逗點做為小數點分隔符號在國際地區設定產生不正確值的問題。 
    * 已修正在 SSDT 中開啟 2008 RS 專案並選擇不升級的問題。 
    * 已修正當資料行型別使用預設格式化以允許從 UI 變更格式化類型時，在 1200 相容性層級模型的導出資料表 UI 中的問題。 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT 6 月 (適用於 SQL Server 2016)  
發行日期︰2016 年 6 月 1 日  
  
組建編號︰14.0.60525.0 

SSDT 公開上市 (GA) 現在已發行。 2016 年 6 月的 SSDT GA 更新加入 SQL Server 2016 RTM 之最新更新的支援，和各種錯誤 (bug) 修正。 如需詳細資訊，請參閱 [2016 年 6 月的 SQL Server Data Tools GA 更新 (英文)](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/)。

      

## <a name="ssdt-april-for-sql-server-2016-rc3"></a>SSDT 4 月 (適用於 SQL Server 2016 RC3)  
發行日期︰2016 年 4 月 15 日  
  
組建編號︰14.0.60413.0  
  
**SQL Server 資料庫**  
* **Always Encrypted 支援︰**對於包含 Always Encrypted 資料行的資料庫，SSDT 和 DacFx 允許檢視和編輯這些資料庫，以及從資料庫專案發行至這些資料庫。 請注意，未來版本將支援變更有資料行加密的資料行。  
* **連接對話方塊和 SQL Server 物件總管︰**多個修正和增強功能。  
    * 列出進階連接屬性的 [詳細資料] 頁面已全面翻修，可在多行方塊中顯示完整的連接字串，並改進對高 DPI 電腦的支援。  
    * 我們已恢復有詳細連線錯誤的傳統錯誤對話方塊。 這有助於利用更清楚的錯誤訊息和堆疊追蹤診斷登入問題，讓 DBA 或 CSS 可取得協助診斷問題所需的資訊。  
    * 對於擁有最小權限的使用者，我們已修正在 [連接] 對話方塊和 SQL Server 物件總管中列出資料庫、檢視 [安全性] 資料夾等等許多問題。  
    * 已改進展開資料庫節點以列出所有資料庫時的 Azure SQL DB 效能。  
* **SSDT 安裝程式︰**  
    * 已修正 .Net 在解除安裝時也在下載的問題。  
    * 現在在高 DPI 的電腦上已正確設定安裝程式的大小。  
    * 已移除如果有較新版本的 SQL Server 則封鎖 SSDT 安裝的版本檢查。  
    * 結構描述比較︰已修正在 Visual Studio 中檢查/取消檢查多個項目花費很長時間的效能問題。  
    * 因為沒有 x86 版本的 SQL Server 2016，支援在 x86 電腦上使用 LocalDB 2014。  
* **建置和部署︰**  
    * 已修正時態表不支援計算資料行的問題。  
    * 部署至 Azure V12 時會忽略 [以單一使用者模式執行部署指令碼] 選項，因為雲端案例中不支援此選項。  
  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc2"></a>SSDT Hotfix (適用於 SQL Server 2016 RC2)  
發行日期︰2016 年 4 月 5 日  
  
組建編號︰14.0.60329.0  
  
此組建包含提供 SQL Server Integration Services 功能的 SSDT 版本 hotfix。 組建 14.0.60316.0 也可搭配 SQL Server 2016 中的 Analysis Services 和 Reporting Services 使用。   
  
若要取得此 hotfix，請使用[此部落格文章的下載連結](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)。  
  
如果報表開發人員使用此組建的 SSDT 建立新報表，請[閱讀已知問題和因應措施](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)了解 SSRS 報表中只在此 hotfix 中找到的暫時性問題。  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc0"></a>SSDT Hotfix (適用於 SQL Server 2016 RC0)  
發行日期︰ 2016 年 3 月 18 日  
  
組建編號︰14.0.60316.0  
  
此組建包含提供 SQL Server 2016 RC0 功能的 SSDT 版本 hotfix。 目前沒有 SSDT 的 RC1 版本。 組建 14.0.60316.0 可以搭配 SQL Server 2016 的 RC0 或 RC1 使用。  
      
## <a name="ssdt-february-2016-preview-for-sql-server-2016-rc0"></a>SSDT 2016 年 2 月預覽 (SQL Server 2016 RC0)  
發行日期︰2016 年 3 月 7 日  
  
組建編號︰14.0.60305.0  
  
-   **SQL Server 專案範本**  
  
    此 SSDT 預覽版本沒有任何宣告。 請參閱 [Database Engine 的新功能](https://msdn.microsoft.com/library/bb510411.aspx)以了解此版本中的其他功能。  
  
-   **SSIS 封裝專案範本**  
  
    SSIS 設計師會建立和維護適用於 SQL Server 2016、2014 或 2012 的封裝。 新範本已重新命名為組件。 SSIS Hadoop 連接器支援 ORC 格式。 請參閱 [Integration Services 的新功能](https://msdn.microsoft.com/library/bb522534.aspx)以取得詳細資料。  
  
-   **SSAS 專案範本 (表格式模型專案)**  
  
    本月份的 Analysis Services 更新提供表格式模型之顯示資料夾的支援，且現在在 SSIS 封裝中支援使用新的 SQL Server 2016 相容性層級建立的任何模型。 如需詳細資訊， 請參閱 [Analysis Services 的新功能 (部落格文章) (英文)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx) 了解詳細資料。  
  
-   **SSRS 報表專案範本**  
  
    此 SSDT 預覽版本沒有任何宣告。 請參閱 [Reporting Services 的新功能](https://msdn.microsoft.com/library/ms170438.aspx)，以了解此版本中的其他功能。  
  
## <a name="ssdt-january-2016-preview"></a>SSDT 2016 年 1 月預覽  
發行日期︰2016 年 2 月 4 日  
  
組建編號︰14.0.60203.0  
  
-   **SQL Server 專案範本**  
  
    此 SSDT 預覽版本沒有任何宣告。 請參閱 [Database Engine 的新功能](https://msdn.microsoft.com/library/bb510411.aspx)以了解此 CTP 中的其他功能。  
  
-   **SSIS 封裝專案範本**  
  
    新增以下支援：ODBC 來源與目的地元件、CDC 控制工作、  
      CDC 來源與分隔器元件、SAP BW 的 Microsoft Connector，以及適用於 Azure 的 Integration Services 功能套件。 請參閱 [Integration Services 的新功能](https://msdn.microsoft.com/library/bb522534.aspx)以取得詳細資料。  
  
-   **SSAS 專案範本**  
  
    包含下列項目的增強功能：1200 相容性層級的表格式模型、DirectQuery 模式中模型的計算結果欄與資料列層級安全性、模型中繼資料的轉譯、SSIS Analysis Services 執行 DDL 工作的 TMSL 指令碼執行，以及許多 Bug 修正。  
    請參閱 [Analysis Services 的新功能 (MSDN)](https://msdn.microsoft.com/library/bb522628.aspx) 或 [Analysis Services 的新功能 (部落格文章) (英文)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx)，以取得詳細資料。  
  
-   **SSRS 報表專案範本**  
  
    此 SSDT 預覽版本沒有任何宣告。 請參閱 [Reporting Services 的新功能](https://msdn.microsoft.com/library/ms170438.aspx)，以了解此 CTP 中的其他功能。  
  
## <a name="ssdt-december-2015-preview"></a>SSDT 2015 年 12 月預覽  
  
-   **SQL Server 專案範本**包括 [連接] 對話方塊、最近歷程記錄清單、載入資料庫清單時連接屬性中驗證內容集正確用法的 Bug 修正。  
  
    -   測試連線逾時值變更為 15 秒。  
  
    -   如果用戶端 IP 在載入資料庫清單時並未註冊，請建立 Azure SQL Database 伺服器。  
  
    -   支援 SQL Server 2016 CTP3.2 程式設計功能。  
  
-   **SSAS 專案範本**新增可根據模型中已定義的 DAX 運算式與其他物件建立導出資料表的支援。  
  
-   **SSIS 封裝專案範本**的新增項目包含 Avro 檔案格式與 Kerberos 驗證的 SSIS Hadoop 連接器支援。   
    請注意本次更新尚未包含支援 SSIS 2012 及 2014 的 SSIS 設計工具。  
  
## <a name="ssdt-november-2015-preview"></a>SSDT 2015 年 11 月預覽  
  
-   **SQL Server 專案範本**。 已針對 SQL Server 和 Azure SQL Database 改善的連線體驗預覽。  
  
-   **SSIS 封裝專案範本**。 SSIS 目錄效能改善：對於 non-ssis-admin 使用者而言，大部分 SSIS 目錄檢視效能已有改善。  
  
-   **SSAS 專案範本**包括 Analysis Services 中表格式模型專案的增強功能。 您可以使用「檢視程式碼」****命令來檢視 JSON 中的模型定義。 如果您並非用 Visual Studio 2015 的完整功能版，可能需要使用此版本才能取得 JSON 編輯器。 您可以免費下載 [Visual Studio Community 版本](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)。  
  
## <a name="ssdt-october-2015-preview"></a>SSDT 2015 年 10 月預覽  
  
-   BI 範本 (Analysis Services 模型、Reporting Services 報表和 Integration Services 套件)。 所有 SQL Server 專案範本都位於一個 SSDT 中。  
  
-   新的 SSIS 功能包括 Hadoop 連接器、控制流程範本，以及資料流程工作的寬鬆緩衝區大小上限。  
  
-   關聯式資料庫專案支援的 SQL Server 2016 CTP 3.0 功能。  
  
-   SSIS 中的各種錯誤修正，以及 Windows 7 OS 適用的支援。  
  
## <a name="ssdt-september-2015-preview"></a>SSDT 2015 年 9 月預覽  
  
-   本預覽中新增多語言支援。  
  
## <a name="ssdt-august-2015-preview"></a>SSDT 2015 年 8 月預覽  
  
-   安裝 SSDT 的新獨立 Setup.exe 程式。  您不需要使用修改過的 SQL Server 安裝程式。 此版本的 SSDT 包含用來建置部署到 SQL Server 或 Azure SQL Database 的關聯式資料庫之專案範本。  
  
## <a name="see-also"></a>另請參閱  
[下載 SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[舊版的 SQL Server Data Tools (SSDT 和 SSDT-BI)](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[Database Engine 的新功能](https://msdn.microsoft.com/library/bb510411.aspx)  
[Analysis Services 的新功能](https://msdn.microsoft.com/library/bb522628.aspx)  
[Integration Services 的新功能](https://msdn.microsoft.com/library/bb522534.aspx)  
  

