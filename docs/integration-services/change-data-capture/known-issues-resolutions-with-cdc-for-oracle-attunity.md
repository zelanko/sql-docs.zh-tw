---
description: Change Data Capture for Oracle by Attunity 的已知錯誤和解決方法
title: Change Data Capture for Oracle by Attunity 的已知錯誤和解決方法 | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 899a00273fbccb1e68e6690556e81bb3f0bde05c
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523903"
---
# <a name="known-errors-and-resolutions-with-change-data-capture-for-oracle-by-attunity"></a>Change Data Capture for Oracle by Attunity 的已知錯誤和解決方法
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]

本主題列出在 Oracle CDC 設計工具這個設定工具中檢視異動資料擷取 (CDC) 執行個體時，最常見問題和已知的解決方法。 此工具是 Change Data Capture for Oracle by Attunity 的一部分，從 SQL Server 2012 開始隨附其中。 

## <a name="bug-fixes"></a>錯誤修正
在花太多時間進行疑難排解之前，請務必使用 CDC for Oracle by Attunity 的最新組建來避免發生已知問題，例如：

### <a name="sql-server-2017"></a>SQL Server 2017

**5.0.0.111 版** 包含下列修正：
- Bug 修正 - 新增 Oracle 資料表時，Oracle CDC 設計工具失敗，並出現「關鍵字 'KEY' 附近的語法不正確」錯誤。 
- 改善 - 改善的 RAC 支援，這包括在 RAC 節點重新啟動時的較佳處理。 
- Bug 修正 - 由於從 v$log 要求 NEXT_CHANGE#，因此 CDC 無法與 Oracle 10.2 搭配運作。 


**5.0.0.93 版** 包含下列修正： 
- 新增 Oracle 資料表時，Microsoft CDC for Oracle by Attunity 設計工具失敗，並出現「關鍵字 'KEY' 附近的語法不正確」錯誤。 

 
### <a name="sql-server-2016"></a>SQL Server 2016

**4.0.107 版** 包含下列修正：
- Bug 修正 – 新增 Oracle 資料表時，Oracle CDC 設計工具失敗，並出現「關鍵字 'KEY' 附近的語法不正確」錯誤。
- 改善 – 改善的 RAC 支援，這包括在 RAC 節點重新啟動時的較佳處理。
- Bug 修正 – 由於從 v$log 要求 NEXT_CHANGE#，因此 CDC 無法與 Oracle 10.2 搭配運作。

**4.0.0.95 版** 包含下列修正： 
- Bug 修正 – 新增 Oracle 資料表時，Oracle CDC 設計工具失敗，並出現「關鍵字 'KEY' 附近的語法不正確」錯誤。

**4.0.0.88 版** 包含下列修正：
-  在 CDC 中新增或移除資料表時，會移除 Attunity CDC 執行個體之 [進階] 選項中新增的屬性。 
- 套用新增 __$command_id 資料行的 SQL 修正之後，Attunity CDC 會停止運作

### <a name="sql-server-2014"></a>SQL Server 2014 

**2.0.0.114 版** 包含下列修正：
- Bug 修正 – 新增 Oracle 資料表時，Oracle CDC 設計工具失敗，並出現「關鍵字 'KEY' 附近的語法不正確」錯誤。
- 改善 – 改善的 RAC 支援，這包括在 RAC 節點重新啟動時的較佳處理。
- Bug 修正 – 由於從 v$log 要求 NEXT_CHANGE#，因此 CDC 無法與 Oracle 10.2 搭配運作。

**2.0.0.92 版** 包含下列修正： 
- 在 CDC 中新增或移除資料表時，會移除 Attunity CDC 執行個體之 [進階] 選項中新增的屬性。 套用新增 __$command_id 資料行的 SQL 修正之後，Attunity CDC 會停止運作
- Oracle 資料表 cdc.table_name 的中繼資料驗證失敗。 資料行 column_name 索引超出範圍。  且下列問題：當您使用 CDC for Oracle by Attunity 時，Oracle CDC 服務會顯示已中止狀態
    - 已於 _SQL Server 2014 RTM 的累計更新 1_ 中修正，如 KB [2894025](https://support.microsoft.com/kb/2894025) 中所述。
- 有些變更會遺失，且不會複寫至 SQL Server 資料庫。 當資料表包含一個以上的字元大型二進位物件 (CLOB)，且其中一個 CLOB 具有大數值時，就會發生此問題。 
    - 已於 _SQL Server 2014 SP1 的累計更新 1_ 和 _SQL Server 2014 RTM 的累計更新 8_ 中修正，如 KB [3029096](https://support.microsoft.com/kb/3029096) 中所述。 
- 當 Oracle 資料表具有 Long 資料類型的資料行時，Change Data Capture for Oracle by Attunity 會停止運作。
    - 已於 _SQL Server 2014 SP1 的累計更新 5_ 和 _SQL 2014 RTM 的累計更新 12_ 中修正，如 KB [3145983](https://support.microsoft.com/kb/3145983) 中所述。

### <a name="sql-server-2012"></a>SQL Server 2012

**1.1.0.102 版** 包含下列修正： 
 
- 在 CDC 中新增或移除資料表時，會移除 Attunity CDC 執行個體之 [進階] 選項中新增的屬性。 套用新增 __$command_id 資料行的 SQL 修正之後，Attunity CDC 會停止運作
- CDC for Oracle 執行個體會在您啟動它時停止回應，且不會擷取變更。 Oracle 伺服器記憶體可能會增加，直到記憶體不足或損毀為止。
- [2672759](https://support.microsoft.com/kb/2672759)：當您使用 Microsoft Change Data Capture for Oracle by Attunity 服務時，出現錯誤訊息："ORA-00600: internal error code"。 新增 SOURCE 層級追蹤，並確認您是否收到相同的 ORA-00600 錯誤。 已由 Oracle 修補程式下載項目修正。
- 多個分割區
    - 當您在 Oracle 資料表上使用超過 10 個分割區時，CDC 執行個體無法擷取資料表的所有變更。 當 Oracle 資料表定義了 10 個以上的分割區時，只會從最後 10 個分割區中擷取變更。 已於 _SQL Server 2012 的 Service Pack 1 版本_ 中修正。 請參閱 [SP1 功能套件下載頁面](https://www.microsoft.com/download/details.aspx?id=35580)。 
- 變更遺失
    - 事件的擷取可能會進入無限迴圈，並停止擷取新的資料變更 (與 Oracle Bug 5623813 相關)。 當 Oracle RAC 環境在執行 CDC 執行個體的停止或繼續時，可能會略過/遺失變更。 這表示 SQL Server 的異動資料擷取將遺失重要資料列，因此資料倉儲或訂閱系統中會遺失資料。 已於 _SQL Server 2012 的 Service Pack 1 版本_ 中修正。 請參閱 [SP1 功能套件下載頁面](https://www.microsoft.com/download/details.aspx?id=35580)
- SQL 中資料行的雙倍寬度
    - 建立 CDC for Oracle 執行個體時，在要針對 SQL Server 執行的指令碼中，可變寬度資料類型資料行長度會是指令碼中所建立 SQL Server 資料表的兩倍。 例如，若您嘗試在 Oracle 資料表的 VARCHAR2(10) 資料行上追蹤變更，則在部署指令碼中，SQL Server 資料表的對應資料行是 NVARCHAR(20)。 於 _SQL Server 2012 SP1 的累計更新 2_ 或 _SQL Server 2012 的累計更新 5_ 中修正，如 KB [2769673](https://support.microsoft.com/kb/2769673) 中所述。 
- 已截斷 DDL 資料
    - 當您針對包含非拉丁字元之 Oracle 資料庫執行大於 4000 個位元組的資料定義語言(DDL) 陳述式時，CDC for Oracle by Attunity 會失敗。 此外，您會看到錯誤訊息 `ORA-01406: fetched column value was truncated.`。 已於 _SQL Server 2012 SP1 的累計更新 4_ 中修正，如 KB [2839806](https://support.microsoft.com/kb/2839806) 中所述。 
- 最後兩個資料行中的變更遺失
    - 已於 _SQL Server 2012 SP1 的累計更新 6_ 中修正，如 KB [2874879](https://support.microsoft.com/kb/2874879) 中所述。 
- 當您使用 CDC for Oracle 時，SQL 交易記錄會增長
     - 設定 Change Data Capture for Oracle 執行個體時，接收已變更資料的 SQL 資料庫將會有鏡像資料表，並將交易標示為複寫。 之所以會發生這種行為，是因為 CDC for Oracle 依賴基礎系統預存程式，而這些程式與 CDC for SQL Server 中使用的程式類似。 不過，由於在單獨使用 CDC for Oracle 時，不涉及任何 SQL CDC 複寫，因此沒有記錄讀取器可清除標示為複寫的交易。 因為交易不需要在 SQL Server 中進行複寫，所以可以使用本文稍後所述的因應措施，以手動方式將交易標示為已散發。 您可以在 KB [2871474](https://support.microsoft.com/kb/2871474) 中找到詳細資訊。 
- 錯誤 `ORACDC000T: Error encountered at position to change event - SCN not found - EOF simulated`。 已於 _SQL Server 2012 SP1 的累計更新 7_ 中修正，如 KB [2883524](https://support.microsoft.com/kb/2883524) 中所述。 
- Oracle 資料表 cdc.table_name 的中繼資料驗證失敗。 資料行 column_name 索引超出範圍。 已於 _SQL Server 2012 SP1 的累計更新 7_ 中修正，如 KB [2883524](https://support.microsoft.com/kb/2883524) 中所述。
- 當您在 SQL Server 2012 中使用 CDC for Oracle by Attunity 時，Oracle CDC 服務會顯示已中止狀態。 已於 _SQL Server 2012 SP1 的累計更新 8_ 中修正，如 KB [2923839](https://support.microsoft.com/kb/2923839) 中所述。  
- 有些變更會遺失，且不會複寫至 SQL Server 資料庫。 當資料表包含一個以上的字元大型二進位物件 (CLOB)，且其中一個 CLOB 具有大數值時，就會發生此問題。 已於 _SQL Server 2012 SP1 的累計更新 8_ 中修正，如 KB [2923839](https://support.microsoft.com/kb/2923839) 中所述。   
- 當 Oracle 資料表具有 Long 資料類型的資料行時，Change Data Capture for Oracle by Attunity 會停止運作。 已於 _SQL Server 2012 SP3 的累計更新 2_ 和 _SQL 2012 SP2 的累計更新 11_ 中修正，如 KB [3145983](https://support.microsoft.com/kb/3145983) 中所述。 

## <a name="collect-detailed-logs"></a>收集詳細記錄 

本節說明如何從 CDC 執行個體收集錯誤和事件。 

### <a name="management-console"></a>管理主控台

在左窗格中醒目提示 CDC 執行個體時，您可以在 Oracle Change Data Capture 設計工具的管理主控台中，看到 [狀態]  訊息欄位中的錯誤。 

### <a name="query-trace-table"></a>查詢追蹤資料表

您可以在 SQL Server 內的 CDC 資料庫中查詢追蹤資料表，以查看記錄的錯誤。 

### <a name="save-output-from-basic-logging"></a>儲存基本記錄的輸出 

若要擷取診斷資訊，請在 Oracle Change Data Capture 管理主控台的 [狀態] 索引標籤上，選取 [收集診斷資訊]  。 

![顯示 Oracle 異動資料擷取管理主控台中 [狀態] 索引標籤的螢幕擷取畫面，其中已標註 [收集診斷資訊] 選項。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

選擇 [開始時間]，並選取記錄檔的位置。 然後選取 [建立]  來啟動診斷資訊收集。 

![[收集 testTA 的診斷資訊] 對話方塊的螢幕擷取畫面。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/start-diagnostics.png)

### <a name="detailed-errors"></a>詳細錯誤

您可以增加執行個體所收集的追蹤層級，並重複執行此案例，以收集更詳細的記錄。 若要這麼做，請選取 [動作] 下的 [屬性]，然後在 [進階] 索引標籤上的 [進階設定] 方格中新增屬性。將屬性的名稱設定為 `trace`，然後將值設定為 `SOURCE`。 

![顯示 [動作] 底下 [屬性] 選項的螢幕擷取畫面。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/properties.png)

重現錯誤，然後選取 [收集診斷資訊]  選項來收集記錄。 

![Oracle 異動資料擷取管理主控台中 [狀態] 索引標籤的另一個螢幕擷取畫面，其中已標註 [收集診斷資訊] 選項。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

## <a name="ora-00942-table-of-view-does-not-exist"></a>ORA-00942 視圖的資料表不存在 

這是 CDC 執行個體的 [狀態]  訊息欄位中所顯示常見錯誤。 此執行個體會重試多次，因此狀態圖示會暫時變成綠色，但之後會失敗並出現紅色驚嘆號和 UNEXPECTED 狀態。 

![顯示 CDC 執行個體 [狀態] 訊息欄位中所顯示常見錯誤的螢幕擷取畫面。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-error.png)

```
"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC508E:Oracle method OCIStmtExecute failed with error: ORA-00942: table or view does not exist ","source","",""

"ERROR","computername","RUNNING","IDLE",
"ORACDC518E:Failed to verify archive log mode.","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC517E:Oracle Call Interface (OCI) method failed: ORA-00942: table or view does not exist .","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC414E:The Engine component failed with return code 1.","engine","",""
```

從 CDC 執行個體連線到 Oracle 伺服器的 Oracle 帳戶沒有查看系統記錄檢視的權限時，就會發生這種情況。 

### <a name="resolution"></a>解決方案

若要解決這個錯誤，請將 Oracle 資料庫系統內適當權限授與目前設定的使用者，或變更用來從 CDC 執行個體連線到 Oracle 伺服器的帳戶。 

安裝程式檔案資料夾 `C:\Program Files\Change Data Capture for Oracle by Attunity\Attunity.SqlServer.XdbCdcDesigner.chm` 中所包含的說明檔中，會詳細說明所有必要權限的清單。  如需完整清單，請參閱 .chm 檔案中標題為＜連線到 Oracle 源資料庫＞的頁面。

您可以從左窗格中選取 CDCInstance，然後在 [CDC 設計工具]  視窗內的 [動作] 最右側窗格中選取 [屬性] 按鈕，以設定使用者帳戶。 您可以從 [屬性] 對話方塊頁面變更 Oracle 記錄挖掘驗證帳戶。

![顯示 [testTA 屬性] 對話方塊的 [Oracle] 索引標籤其螢幕擷取畫面。](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-connection.png)


  
## <a name="see-also"></a>請參閱  
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [使用變更資料 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [管理和監視異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
