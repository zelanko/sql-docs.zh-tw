---
title: "SQL Server 2012 SP4 版本資訊 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "0"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b09784b129109f907c19a56a2a6fadcba119e73d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-2012-sp4-release-notes"></a>SQL Server 2012 SP4 版本資訊
本主題摘要說明 SQL Server 2012 SP4 中所包含的改善。 本主題也說明安裝 SP4 或針對 SP4 安裝進行疑難排解之前所要檢閱的問題。 版本資訊僅於線上提供，安裝媒體中並不提供。 我們會在發現問題時定期更新本主題。 如需 SP4 中修正的詳細清單，請參閱 [SQL Server 2012 SP4 發行資訊](https://go.microsoft.com/fwlink/?linkid=846937)。  

> Service Pack 4 包含所有 SQL Server 2012 SP3 累積更新。
  
##<a name="download-pages"></a>下載頁面
下列項目連結至 SQL Server 2012 SP3 的主要下載套件。 下載頁面會提供系統需求與基本安裝指示。
- [SQL Server 2012 SP4 修補程式安裝](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 Feature Pack](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>SP4 效能和規模改善

- **已改善散發代理程式清除程序** - 過大的散發資料庫會造成封鎖和死結情況。 改善的清除程序旨在排除其中一些封鎖或死結情況。 
- **動態記憶體物件調整** - 根據節點與核心數目動態分割記憶體物件，以在新式硬體上調整規模。 動態升級的目標是為了防止潛在的瓶頸，並自動分割安全執行緒記憶體物件。 未分割的記憶體物件可動態升級成依節點進行分割。 資料分割數目等於 NUMA 節點數目。 依節點分割的記憶體物件可進一步升級成依 CPU 進行分割，其中資料分割數目等於 CPU 數目。
- **針對緩衝集區啟用 > 8 TB** - 針對緩衝集區使用量啟用 128 TB 的虛擬位址空間
- **變更追蹤清除** - 已提升變更追蹤端資料表的變更追蹤清除效能和效率。 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>SP4 可支援性和診斷改善

- **複寫代理程式的完整傾印支援** - 現在，如果複寫代理程式發生未處理的例外狀況，預設行為是建立例外狀況徵兆的小型傾印。 預設行為需要針對未處理的例外狀況進行複雜的疑難排解步驟。 SP4 引進新的登錄機碼，以支援建立複寫代理程式的完整傾印。
- **已增強執行程序表 XML 中的診斷** - 已增強執行程序表 XML 來公開已啟用之追蹤旗標、最佳化巢狀迴圈聯結之記憶體片段、CPU 時間和已耗用時間的相關資訊。 
- **診斷 XE 和 DMV 之間的更佳關聯性** - 使用 Query_hash 和 query_plan_hash 欄位來唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL Server 沒有「不帶正負號的 Bigint」，因此轉型不一定會運作正常。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行，不同之處在於這些資料行是定義為 INT64，以協助建立 XE 和 DMV 之間的查詢關聯。 
- **更佳的記憶體授與/使用量診斷** - 新增 query_memory_grant_usage XEvent (Server 2016 SP1 中的 backport)
- **將通訊協定追蹤新增至 SSL 交涉步驟** - 新增成功/失敗交涉的位元追蹤資訊，包括通訊協定等。針對連線案例 (例如部署 TLS 1.2) 進行疑難排解時可能會很有用
- **為散發資料庫設定正確的相容性層級** - 在 Service Pack 安裝之後，散發資料庫相容性層級會變更為 90。 此層級變更是由於 sp_vupgrade_replication 預存程序中的某個問題所致。 SP 現在已經過變更，可為散發資料庫設定正確的相容性層級。 
- **新增用於複製資料庫的 DBCC 命令** - 複製資料庫是新增的 DBCC 命令，允許 CSS 等進階使用者藉由複製結構描述和中繼資料 (而不是資料)，來為現有的生產環境資料庫進行疑難排解。 此呼叫是透過 DBCC clonedatabase (‘source_database_name’, ‘clone_database_name’) 來執行。 請勿在生產環境中使用複製的資料庫。 若要查看某個資料庫是否透過複製資料庫的呼叫所產生，請選取 DATABASEPROPERTYEX('clonedb', 'isClone')。傳回值 1 表示 true，0 表示 false。 
- **SQL 錯誤記錄檔中的 TempDB 檔案和檔案大小資訊** - 如果 TempDB 資料檔案在啟動期間的大小和自動成長不同，則會列印檔案數目並觸發警告。
- **SQL Server 錯誤記錄檔中的 IFI 支援訊息** - 在錯誤記錄檔中指出已啟用/停用 [資料庫立即檔案初始化]
- **新增 DMF 以取代 DBCC INPUTBUFFER** - 引進以 session_id 作為參數的新動態管理函數 sys.dm_input_buffer 來取代 DBCC INPUTBUFFER
- **針對可用性群組的讀取路由失敗增強 XEvent** - 目前，只有存在路由清單，但路由清單中沒有伺服器可供連接時，才會引發 read_only_rout_fail XEvent。 這項改善包含其他資訊以協助進行疑難排解，它也會在引發 XEvent 的字碼指標上展開。 
- **已改善使用可用性群組容錯移轉處理 Service Broker 的功能** - 目前，在 AG 容錯移轉期間啟用可用性群組資料庫上的 Service Broker 時，所有來自主要複本的 Service Broker 連接都會保持開啟狀態。 這項改善會關閉所有在 AG 容錯移轉期間開啟的這類連接。
- **[自動軟體式 NUMA 資料分割](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)** - 在 SQL 2014 SP2 中，於伺服器層級啟用追蹤旗標 8079 時引進了自動軟體式 NUMA。 在啟動期間啟用追蹤旗標 8079 時，SQL Server 2014 SP2 會查閱硬體配置，並在系統報告每個 NUMA 節點上有 8 個或更多個 CPU 時自動設定軟體式 NUMA。 自動軟體式 NUMA 會以感知超執行緒 (HT/邏輯處理器) 的方式運作。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議先使用自動軟體式 NUMA 測試工作負載的效能，再於生產環境中將它開啟。

## <a name="see-also"></a>另請參閱
- [安裝 SQL Server 2012 服務更新](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [如何識別 SQL Server 版本與版本類型](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
