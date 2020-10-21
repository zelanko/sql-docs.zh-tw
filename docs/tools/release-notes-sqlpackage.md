---
title: DacFx 和 SqlPackage 版本資訊
description: Microsoft sqlpackage 的版本資訊。
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: 90485210bbc0fe657516306dd433f3241b5c90c9
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005977"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe 的版本資訊

**[下載最新版本](sqlpackage-download.md)**

本文會列出 SqlPackage.exe 發行版本所提供的功能與修正。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="186-sqlpackage"></a>18.6 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2143544)|2020 年 9 月 18 日|18.6|15.0.4897.1|
|macOS .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2143659)|2020 年 9 月 18 日| 18.6|15.0.4897.1|
|Linux .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2143497)|2020 年 9 月 18 日| 18.6|15.0.4897.1|
|Windows .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2143496)|2020 年 9 月 18 日| 18.6|15.0.4897.1|

### <a name="features"></a>特性
| 功能 | 詳細資料 |
| :------ | :------ |
| 平台 | 已將 .NET Core 版本的 sqlpackage 更新為 .NET Core 3.1 |
| Always Encrypted | 已新增 SQL Server 2019 的安全記憶體保護區匯入和匯出支援 |
| 部署 | 已新增支援在從 Azure SQL Database 匯出時忽略已啟用變更資料擷取的資料表 |
| 部署 | 已在 Azure SQL Database 中新增索引選項 OPTIMIZE_FOR_SEQUENTIAL_KEY 的支援 |
| 部署 | 已新增 Azure Synapse Analytics 的識別欄位支援 | 
| [說明] | 輸出 help (/?) 中的 sqlpackage 版本並支援 /version 參數 | 

### <a name="fixes"></a>修正
| 功能 | 詳細資料 |
| :------ | :------ | 
| 部署 | 以非系統管理員 (sysadmin) 使用者身分修正以 Azure SQL Database 受控執行個體作為目標時所產生的錯誤部署指令碼  | 
| 部署 | 已修正在執行指令碼動作時載入部署參與者的問題 | 
| [說明] | 當作業花費的時間超過 1 天時，在 sqlpackage 中輸出正確的經歷時間 | 
| 部署 | 已修正針對 .NET Core 部署時的 dacpac 註冊問題 | 
| 部署 | 已修正 .NET Core 處理 /accessToken (/at) 參數時的 sqlpackage | 
| 部署 | 允許預存程序中的 ALTER TABLE 陳述式作為非最上層陳述式 | 
| 部署 | 已將具體化檢視的 Azure Synapse Analytics 驗證修正為不區分大小寫 | 

### <a name="known-issues"></a>已知問題
| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 尚不支援 Azure Synapse Analytics 工作負載管理功能 (工作負載群組和工作負載分類器) | 

## <a name="1851-sqlpackage"></a>18.5.1 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2134206)|2020 年 6 月 24 日|18.5.1|15.0.4826.1|
|macOS .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2134312)|2020 年 6 月 24 日| 18.5.1|15.0.4826.1|
|Linux .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2134311)|2020 年 6 月 24 日| 18.5.1|15.0.4826.1|
|Windows .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2134310)|2020 年 6 月 24 日| 18.5.1|15.0.4826.1|

### <a name="fixes"></a>修正
| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 已修正 18.5 中引入的迴歸問題：透過外部登入使用者在內部部署中部署 dacpac 或匯入 bacpac 時，會出現「'type' 附近的語法不正確」的錯誤 | 

## <a name="185-sqlpackage"></a>18.5 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2128142)|2020 年 4 月 28 日|18.5|15.0.4769.1|
|macOS .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2128145)|2020 年 4 月 28 日| 18.5|15.0.4769.1|
|Linux .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2128144)|2020 年 4 月 28 日| 18.5|15.0.4769.1|
|Windows .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2128143)|2020 年 4 月 28 日| 18.5|15.0.4769.1|

### <a name="features"></a>特性
| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | SQL Server 2008 及更新版本、Azure SQL Database 和 Azure Synapse Analytics 現已支援資料敏感度分類 |
| 部署 | 新增 Azure Synapse Analytics 的資料表條件約束支援 |
| 部署 | 新增 Azure Synapse Analytics 的已排序叢集資料行存放區索引支援 |
| 部署 | 新增外部資料來源 (適用於 Oracle、Teradata、MongoDB/CosmosDB、ODBC、巨量資料叢集) 的支援，以及 SQL Server 2019 巨量資料叢集的外部資料表 |
| 部署 | 新增 SQL Database Edge 執行個體作為支援的版本 |
| 部署 | 支援格式為 '\<server>.\<dnszone>.database.windows.net' 的受控執行個體伺服器名稱 |
| 部署 | 在 Azure Synapse Analytics 中新增複製命令支援 |
| 部署 | 新增發佈期間的部署選項 'IgnoreTablePartitionOptions'，以避免當 Azure Synapse Analytics 資料表上的資料分割函數變更時重新建立資料表 |
| .NET Core | 新增 .NET Core 版本 sqlpackage 中 Microsoft.Data.SqlClient 的支援 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正
| 修正 | 詳細資料 |
| :-- | :------ |
| 部署 | 修正將 JSON 路徑剖析為運算式 |
| 部署 | 修正產生 AlterAnyDatabaseScopedConfiguration 和 AlterAnySensitivityClassification 權限的 GRANT 陳述式 |
| 部署 | 修正無法辨識的外部指令碼權限 |
| 部署 | 修正內嵌屬性 - 屬性的隱含新增不應顯示差異，但明確提及應透過指令碼顯示 |
| 部署 | 已解決變更具體化檢視 (MV) 參考放資料表會產生 Azure Synapse Analytics MV 不支援的 Alter View 陳述式此問題 |
| 部署 | 修正將資料行新增至具有 Azure Synapse Analytics 資料的資料表時發佈失敗此問題 |
| 部署 | 修正變更 Azure Synapse Analytics 的發佈資料行類型 (資料遺失案例) 時，更新指令碼應將資料移至新的資料表此問題 |
| ScriptDom | 修正 ScriptDom Bug，此 Bug 導致其無法辨識在內嵌索引後面定義的內嵌條件約束 |
| ScriptDom | 修正 ScriptDom SYSTEM_TIME 在批次陳述式中遺漏右括弧 |
| Always Encrypted | 修正 sqlpackage 重新連線且暫存資料表已消失時無法卸除 #tmpErrors 資料表，因為暫存資料表會在連線停止時消失 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題
| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 |  18.5 中引入的迴歸，在透過外部登入使用者在內部部署中部署 dacpac 或匯入 bacpac 時，會導致「'type' 附近的語法不正確」的錯誤。 因應措施是使用 sqlpackage 18.4，這將在下一版 sqlpackage 中修正。 | 
| .NET Core | 因為 Microsoft.Data.SqlClient 的此一[已知問題](https://github.com/dotnet/SqlClient/issues/559)，匯入包含敏感度分類的 bacpacs 時，會因「內部連接發生嚴重錯誤」而失敗。 這將在下一版 sqlpackage 中修正。 |
| &nbsp; | &nbsp; |

## <a name="1841-sqlpackage"></a>18.4.1 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2113703)|2019 年 12 月 13 日|18.4.1|15.0.4630.1|
|macOS .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2113705)|2019 年 12 月 13 日| 18.4.1|15.0.4630.1|
|Linux .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2113331)|2019 年 12 月 13 日| 18.4.1|15.0.4630.1|
|Windows .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2113704)|2019 年 12 月 13 日| 18.4.1|15.0.4630.1|

### <a name="fixes"></a>修正
| 修正 | 詳細資料 |
| :-- | :------ |
| ScriptDom |  18.3.1 中引進的 ScriptDom 剖析迴歸誤將 'RENAME' 視為最上層權杖，因而導致剖析失敗。
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題 

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 |  18.4.1 中所引進迴歸會導致在外部登入的使用者部署 dacpac 或匯入 bacpac 時， 發生「物件參考未設定成物件的執行個體」錯誤。 因應措施是使用 sqlpackage 18.4，這將在下一版 sqlpackage 中修正。 | 
| &nbsp; | &nbsp; |

## <a name="184-sqlpackage"></a>18.4 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2108813)|2019 年 10 月 29 日|18.4|15.0.4573.2|
|macOS .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2108815)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Linux .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2108814)|2019 年 10 月 29 日| 18.4|15.0.4573.2|
|Windows .NET Core |[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2109019)|2019 年 10 月 29 日| 18.4|15.0.4573.2|

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 新增部署至 Azure Synapse Analytics 的支援 (GA)。 | 
| 平台 | 適用於 macOS、Linux 和 Windows 的 sqlpackage .NET Core GA。 | 
| 安全性 | 移除 SHA1 程式碼簽署。 |
| 部署 | 新增支援全新的 Azure 資料庫版本：GeneralPurpose、BusinessCritical、Hyperscale |
| 部署 | 新增對 Azure Active Directory 使用者和群組的受控執行個體支援。 |
| 部署 | 支援 .NET Core 上 sqlpackage 的 /AccessToken 參數。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題 

| 功能 | 詳細資料 |
| :------ | :------ |
| ScriptDom |  18.3.1 中引進的 ScriptDom 剖析迴歸誤將 'RENAME' 視為最上層權杖，因而導致剖析失敗。 這將在下一版 sqlpackage 中修正。 | 
| &nbsp; | &nbsp; |

### <a name="known-issues-for-net-core"></a>.NET Core 的已知問題

| 功能 | 詳細資料 |
| :------ | :------ |
| 匯入 |  針對壓縮檔大小超過 4 GB 的 .bacpac 檔案，您可能需要使用 .NET Core 版本的 sqlpackage 來執行匯入。  因為 .NET Core 會產生 ZIP 標頭，這些標頭雖然有效，但 .NET Full Framework 版本的 sqlpackage 無法讀取。 | 
| 部署 | 不支援 /p:Storage=File 參數。 .NET Core 只支援記憶體。 | 
| Always Encrypted | sqlpackage .NET Core 不支援 Always Encrypted 資料行。 | 
| 安全性 | sqlpackage .NET Core 不支援多重要素驗證的 /ua 參數。 | 
| 部署 | 不支援使用 JSON 資料序列化的舊版 V2 .dacpac 與 .bacpac 檔案。 |
| &nbsp; | &nbsp; |

## <a name="1831-sqlpackage"></a>18.3.1 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2102893)|2019 年 9 月 13 日|18.3.1|15.0.4538.1|
|macOS .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102894)|2019 年 9 月 13 日| 18.3.1|15.0.4538.1|
|Linux .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102978)|2019 年 9 月 13 日| 18.3.1|15.0.4538.1|
|Windows .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102979)|2019 年 9 月 13 日| 18.13.1|15.0.4538.1|

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 新增部署至 Azure Synapse Analytics 的支援 (預覽)。 | 
| 部署 | 將 /p:DatabaseLockTimeout=(INT32 '60') 參數新增至 sqlpackage。 | 
| 部署 | 將 /p:LongRunningCommandTimeout=(INT32) 參數新增至 sqlpackage。 |
| 匯出/解壓縮 | 將 /p:TempDirectoryForTableData=(STRING) 參數新增至 sqlpackage。 |
| 部署 | 允許從其他位置載入部署參與者。 系統會從部署目標 .dacpac 的相同目錄 (相對於 sqlpackage 二進位檔的 Extensions 目錄) 載入部署參與者，並將 /p:AdditionalDeploymentContributorPaths=(STRING) 參數新增至可指定其他目錄位置的 sqlpackage 中。 |
| 部署 | 新增支援 OPTIMIZE_FOR_SEQUENTIAL_KEY。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 部署 | 修正以忽略自動索引，使其不會在部署時中斷。 | 
| Always Encrypted | 修正以處理 Always Encrypted varchar 資料行。 | 
| 建置/部署 | 修正以解析 XML 資料行集的 nodes() 方法。| 
| ScriptDom | 修正會誤將 'URL' 字串解譯為最上層權杖的其他案例。 | 
| 圖形 | 修正條件約束中虛擬資料行參考所產生的 TSQL。  | 
| 匯出 | 產生符合複雜性需求的隨機密碼。 | 
| 部署 | 修正以在擷取條件約束時接受命令逾時。 | 
| .NET Core (預覽) | 修正檔案的診斷記錄。 | 
| .NET Core (預覽) | 使用串流來匯出資料表資料，以支援大型資料表。 | 
| &nbsp; | &nbsp; |

## <a name="182-sqlpackage"></a>18.2 sqlpackage

|平台|下載|發行日期|版本|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2087429)|2019 年 4 月 15 日|18.2|15.0.4384.2|
|macOS .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2087247)|2019 年 4 月 15 日 | 18.2 |15.0.4384.2|
|Linux .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2087431)|2019 年 4 月 15 日 | 18.2 |15.0.4384.2|

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 圖形 | 針對邊緣條件約束與邊緣條件約束子句新增圖形資料表支援。 |
| 部署 | 已啟用模型驗證規則，以針對 SQL Server 2016 和更新版本支援 32 個索引鍵資料行。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 部署 | 修正因為使用了不支援的查詢提示，而對 SQL Server 2016 RTM 資料庫進行反向工程。 |
| 部署 | 修正在建立檔案群組陳述式前發生之自動關閉 alter 陳述式的部署順序。 |
| ScriptDom | 修正 ScriptDom 剖析迴歸，其中會將 'URL' 字串解譯為最上層權杖。 |
| 部署 | 修正在剖析 alter 資料表新增 index 陳述式時的 Null 參考例外狀況。 | 
| 結構描述比較 | 已針對一律顯示為不同且可為 Null 之保存的計算資料行修正結構描述比較。|
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

發行日期：&nbsp; 2019 年 2 月 1 日  
組建：&nbsp; 15.0.4316.1  
預覽版本。

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 已新增 UTF8 定序的支援。 |
| 部署 | 在索引檢視表上啟用了非叢集資料行存放區索引。 |
| 平台 | 移到 .NET Core 2.2。 | 
| 結構描述比較 | 在 .NET Core 上使用記憶體支援的儲存體來進行結構描述比較。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 效能 | 使用舊版基數估計工具進行反向工程查詢的效能修正。 | 
| 效能 | 已修正在產生指令碼時所發生的重大結構描述比較效能問題。 | 
| 結構描述比較 | 已修正結構描述漂移偵測邏輯，以忽略特定的擴充事件 (xevent) 工作階段。 |
| 圖形 | 已修正圖形資料表的匯入順序。 | 
| 匯出 | 已修正搭配物件權限匯出外部資料表。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

此版本包含目標為 .NET Core 2.2 之 sqlpackage 的跨平台預覽組建。 Sqlpackage 可以在 macOS 和 Linux 上執行。

| 已知問題 | 詳細資料 |
| :---------- | :------ |
| 部署 | 針對 .NET Core，不支援建置及部署參與者。 | 
| 部署 | 針對 .NET Core，不支援使用 JSON 資料序列化的舊版 .dacpac 與 .bacpac 檔案。 | 
| 部署 | 針對 .NET Core，由於發生區分大小寫的檔案系統問題，因此可能無法解析參考的 .dacpacs (例如 master.dacpac)。 | 因應措施是將參考檔案的名稱改為大寫 (例如 MASTER.BACPAC)。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

發行日期：&nbsp; 2018 年 10 月 24 日  
組建：&nbsp; 15.0.4200.1

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 | 已新增資料庫相容性層級 150 的支援。 | 
| 部署 | 已新增受控執行個體的支援。 | 
| 效能 | 已新增 MaxParallelism 命令列參數，可指定資料庫作業的平行處理原則程度。 | 
| 安全性 | 已新增 AccessToken 命令列參數，可指定連線至 SQL Server 時的驗證權杖。 | 
| 匯入 | 已新增支援串流處理 BLOB/CLOB 資料類型以用於匯入。 | 
| 部署 | 已新增純量 UDF 'INLINE' 選項的支援。 | 
| 圖形 | 已新增圖形資料表 'MERGE' 語法的支援。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 圖形 | 已針對圖形資料表修正無法解析的虛擬資料行。 |
| 部署 | 已修正在使用記憶體最佳化的資料表時，透過記憶體最佳化的檔案群組來建立資料庫。 |
| 部署 | 已修正在外部資料表上包含擴充屬性。 |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

發行日期：&nbsp; 2018 年 6 月 22 日  
組建：&nbsp; 14.0.4079.2

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 診斷 | 已改進連線失敗的錯誤訊息，包括 SqlClient 例外狀況訊息。 |
| 部署 | 在單一分割區索引上支援索引壓縮以用於匯入/匯出。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 部署 | 已修正使用 SQL 2017 和更新版本的 XML 資料行集的反向工程問題。 | 
| 部署 | 已針對 Azure SQL Database 修正對資料庫相容性層級 140 進行指令碼處理會遭到忽略的問題。 |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

發行日期：&nbsp; 2018 年 1 月 25 日  
組建：&nbsp; 14.0.3917.1

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 匯入/匯出 | 已新增 ThreadMaxStackSize 命令列參數，可使用大量巢狀陳述式來剖析 Transact-SQL。 |
| 部署 | 資料庫目錄定序支援。 | 
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 匯入 | 將 Azure SQL Database .bacpac 匯入至內部部署執行個體時，已修正因為「此版本的 SQL Server 不支援沒有密碼的資料庫主要金鑰」  而引發的錯誤。 |
| 圖形 | 已針對圖形資料表修正無法解析的虛擬資料行錯誤。 |
| 結構描述比較 | 已修正用來比較結構描述的 SQL 驗證。 | 
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

發行日期：&nbsp; 2017 年 12 月 12 日  
組建：&nbsp; 14.0.3881.1

### <a name="features"></a>特性

| 功能 | 詳細資料 |
| :------ | :------ |
| 部署 |  已在 SQL 2017+ 和 Azure SQL Database 上新增「時態性保留原則」  的支援。 | 
| 診斷 | 已新增 /DiagnosticsFile:"C:\Temp\sqlpackage.log" 命令列參數，可指定要儲存診斷資訊的檔案路徑。 | 
| 診斷 | 已新增 /Diagnostics 命令列參數，可將診斷資訊記錄至主控台。 |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| 修正 | 詳細資料 |
| :-- | :------ |
| 部署 | 在遇到不了解的資料庫相容性層級時不要封鎖。 相反地，將假設為最新的 Azure SQL Database 或內部部署平台。 |
| &nbsp; | &nbsp; |
