---
title: SQL Server 2012 Service Pack 版本資訊 | Microsoft Docs
ms.prod: sql
ms.technology: install
ms.custom: ''
ms.date: 02/26/2018
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: e06daf1c4963df2706781ba222ef5efd07ab9249
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112376"
---
# <a name="sql-server-2012-service-pack-release-notes"></a>SQL Server 2012 Service Pack 版本資訊
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
本主題包含四個 SQL Server 2012 Service Pack 的彙總版本資訊。 每個 Service Pack 都會累積先前的 Service Pack。

Service Pack 僅於線上提供，安裝媒體上並不提供，並可依下列方式下載：
- [SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846937)
- [SQL Server 2012 SP3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)
- [SQL Server 2012 SP2](https://support.microsoft.com/KB/2958429)
- [SQL Server 2012 SP1](https://go.microsoft.com/fwlink/p/?LinkID=268158)

## <a name="service-pack-4-release-notes"></a>Service Pack 4 版本資訊

### <a name="download-pages"></a>下載頁面

- [SQL Server 2012 SP4 Feature Pack](https://www.microsoft.com/download/details.aspx?id=56041)
- [SQL Server 2012 SP4 修補程式安裝](https://www.microsoft.com/download/details.aspx?id=56040)
- [SQL Server 2012 SP4 Express](https://www.microsoft.com/download/details.aspx?id=56042)


### <a name="performance-and-scale-improvements"></a>效能和規模改進
- **已改善散發代理程式清除程序** - 過大的散發資料庫會造成封鎖和死結情況。 改善的清除程序旨在排除其中一些封鎖或死結情況。 
- **動態記憶體物件調整** - 根據節點與核心數目動態分割記憶體物件，以在新式硬體上調整規模。 動態升級的目標是為了防止潛在的瓶頸，並自動分割安全執行緒記憶體物件。 未分割的記憶體物件可動態升級成依節點進行分割。 資料分割數目等於 NUMA 節點數目。 依節點分割的記憶體物件可進一步升級成依 CPU 進行分割，其中資料分割數目等於 CPU 數目。
- **針對緩衝集區啟用 > 8 TB** - 針對緩衝集區使用量啟用 128 TB 的虛擬位址空間
- **變更追蹤清除** - 已提升變更追蹤端資料表的變更追蹤清除效能和效率。 

### <a name="supportability-and-diagnostics-improvements"></a>可支援性和診斷改進
- **複寫代理程式的完整傾印支援** - 現在，如果複寫代理程式發生未處理的例外狀況，預設行為是建立例外狀況徵兆的小型傾印。 預設行為需要針對未處理的例外狀況進行複雜的疑難排解步驟。 SP4 引進新的登錄機碼，以支援建立複寫代理程式的完整傾印。
- **已增強執行程序表 XML 中的診斷** - 已增強執行程序表 XML 來公開已啟用之追蹤旗標、最佳化巢狀迴圈聯結之記憶體片段、CPU 時間和已耗用時間的相關資訊。 
- **診斷 XE 和 DMV 之間的更佳關聯性** - 使用 Query_hash 和 query_plan_hash 欄位來唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL Server 沒有「不帶正負號的 Bigint」，因此轉型不一定會成功。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行，不同之處在於這些資料行是定義為 INT64，以協助建立 XE 和 DMV 之間的查詢關聯。 
- **更佳的記憶體授與/使用量診斷** - 新增 query_memory_grant_usage XEvent (Server 2016 SP1 中的 backport)
- **將通訊協定追蹤新增至 SSL 交涉步驟** - 新增成功/失敗交涉的位元追蹤資訊，包括通訊協定等。針對連線案例 (例如部署 TLS 1.2) 進行疑難排解時可能會很有用
- **為散發資料庫設定正確的相容性層級** - 在 Service Pack 安裝之後，散發資料庫相容性層級會變更為 90。 此層級變更是由於 sp_vupgrade_replication 預存程序中的某個問題所致。 SP 現在已經過變更，可為散發資料庫設定正確的相容性層級。 
- **新增用於複製資料庫的 DBCC 命令** - 複製資料庫是新增的 DBCC 命令，允許 CSS 等進階使用者藉由複製結構描述和中繼資料 (而不是資料)，來為現有的生產環境資料庫進行疑難排解。 此呼叫是透過 DBCC clonedatabase ('source_database_name', 'clone_database_name') 來執行。 請勿在生產環境中使用複製的資料庫。 若要查看某個資料庫是否透過複製資料庫的呼叫所產生，請選取 DATABASEPROPERTYEX('clonedb', 'isClone')。傳回值 1 表示 true，0 表示 false。 
- **SQL 錯誤記錄檔中的 TempDB 檔案和檔案大小資訊** - 如果 TempDB 資料檔案在啟動期間的大小和自動成長不同，則會列印檔案數目並觸發警告。
- **SQL Server 錯誤記錄檔中的 IFI 支援訊息** - 在錯誤記錄檔中指出已啟用/停用 [資料庫立即檔案初始化]
- **新增 DMF 以取代 DBCC INPUTBUFFER** - 引進以 session_id 作為參數的新動態管理函數 sys.dm_input_buffer 來取代 DBCC INPUTBUFFER
- **針對可用性群組的讀取路由失敗增強 XEvent** - 目前，只有存在路由清單，但路由清單中沒有伺服器可供連接時，才會引發 read_only_rout_fail XEvent。 這項改善包含其他資訊以協助進行疑難排解，它也會在引發 XEvent 的字碼指標上展開。 
- **已改善使用可用性群組容錯移轉處理 Service Broker 的功能** - 目前，在 AG 容錯移轉期間啟用可用性群組資料庫上的 Service Broker 時，所有來自主要複本的 Service Broker 連接都會保持開啟狀態。 這項改善會關閉所有在 AG 容錯移轉期間開啟的這類連接。
- **自動軟體式 NUMA 資料分割** - 在 SQL 2014 SP2 中，於伺服器層級啟用追蹤旗標 8079 時會導入自動[軟體式 NUMA](../database-engine/configure-windows/soft-numa-sql-server.md) 資料分割。 在啟動期間啟用追蹤旗標 8079 時，SQL Server 2014 SP2 會查閱硬體配置，並在系統報告每個 NUMA 節點上有 8 個或更多個 CPU 時自動設定軟體式 NUMA。 自動軟體式 NUMA 會以感知超執行緒 (HT/邏輯處理器) 的方式運作。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議先使用自動軟體式 NUMA 測試工作負載的效能，再於生產環境中將它開啟。

## <a name="service-pack-3-release-notes"></a>Service Pack 3 版本資訊

### <a name="download-pages"></a>下載頁面
- [SQL Server 2012 SP3 Feature Pack](https://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](https://go.microsoft.com/fwlink/?linkid=692144)

如需詳細資訊以根據您目前安裝的版本識別要下載的檔案名稱與位置，請參閱 [SQL Server 2012 Service Pack 3 版本資訊](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)中的＜選取正確的下載檔案＞一節。

## <a name="service-pack-2-release-notes"></a>Service Pack 2 版本資訊
  
### <a name="download-pages"></a>下載頁面 
- [SQL Server 2012 SP2 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](https://go.microsoft.com/fwlink/?LinkID=401007)

使用下表，根據您目前安裝的版本來識別要下載的檔案位置與名稱。 下載頁面會提供系統需求與基本安裝指示。  

|如果您目前安裝的版本是...|而您要...|請下載並安裝...|  
|---|---|---|   
|32 位元安裝：|||  
|任何 SQL Server 2012 版本的 32 位元版本|升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 下載頁面**<arch> **-** <lang id>**的** SQLServer2012SP2-KB2958429- [.exe](https://go.microsoft.com/fwlink/?LinkID=401006)|  
|32 位元版本的 SQL Server 2012 RTM Express|升級為 32 位元版本的 SQL Server 2012 Express SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的 SQL Server 2012 Management Studio Express|升級為 32 位元版本的 SQL Server 2012 SP2 Management Studio Express|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32 位元版本的任何 SQL Server 2012 版本，以及 32 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 32 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPRADV_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)。|  
|來自 [Microsoft SQL Server 2012 RTM 功能套件](https://www.microsoft.com/download/details.aspx?id=29065) 或 [Microsoft SQL Server 2012 SP1 功能套件](https://go.microsoft.com/fwlink/p/?LinkID=268266)的一或多個 32 位元版本的工具|將工具升級為 32 位元版本的 Microsoft SQL Server 2012 SP2 功能套件|來自 Microsoft [SQL Server 2012 SP2 功能套件下載頁面](https://go.microsoft.com/fwlink/?LinkID=401008)的一個或多個工具|  
|64 位元安裝：|||  
|任何 SQL Server 2012 版本的 64 位元版本|升級為 64 位元版本的 SQL Server 2012 SP2|來自<arch>-<langid>SQL Server 2012 SP2 下載頁面 [的 SQLServer2012SP2-KB2958429-](https://go.microsoft.com/fwlink/?LinkID=401006).exe|  
|64 位元版本的 SQL Server 2012 RTM Express|升級為 64 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|64 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 64 位元版本的 SQL Server 2012 SP2|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|64 位元版本的 SQL Server 2012 Management Studio Express|升級為 64 位元版本的 SQL Server 2012 SP2 Management Studio Express|**SQL Server 2012 SP2 Express 下載頁面**<arch>**的**<lang>**SQLEXPR_** SQLServer2012SP2-KB2958429- [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|來自 [Microsoft SQL Server 2012 RTM 功能套件](https://www.microsoft.com/download/details.aspx?id=29065) 或 [Microsoft SQL Server 2012 SP1 功能套件](https://go.microsoft.com/fwlink/p/?LinkID=268266)的一或多個 64 位元版本的工具|將工具升級為 64 位元版本的 Microsoft SQL Server 2012 SP2 功能套件|來自 Microsoft [SQL Server 2012 SP2 功能套件下載頁面](https://go.microsoft.com/fwlink/?LinkID=401008)的一個或多個工具|   


## <a name="service-pack-1-release-notes"></a>Service Pack 1 版本資訊

### <a name="download-pages"></a>下載頁面  
- [SQL Server 2012 SP1 Feature Pack](https://go.microsoft.com/fwlink/p/?LinkID=268158)
- [SQL Server 2012 SP1 Express](https://www.microsoft.com/download/details.aspx?id=35579)


您可以使用下表來決定要下載並安裝的檔案。 在安裝 Service Pack 之前，請先確認您擁有正確的系統需求。 系統需求會列在資料表中所連結的下載頁面。  

|如果您目前安裝的版本是...|而您要...|請下載並安裝...|  
|---|---|---|  
|**32 位元安裝：**|||  
|任何 SQL Server 2012 版本的 32 位元版本|升級為 32 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32 位元版本的 SQL Server 2012 RTM Express|升級為 32 位元版本的 SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 32 位元版本的 SQL Server 2012 SP1|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|32 位元版本的 SQL Server 2012 Management Studio Express|升級為 32 位元版本的 SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|32 位元版本的任何 SQL Server 2012 版本， **以及** 32 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 32 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|[Microsoft SQL Server 2012 RTM 功能套件](https://www.microsoft.com/download/details.aspx?id=44272)中一個或多個 32 位元版本的工具|將工具升級為 32 位元版本的 Microsoft SQL Server 2012 SP1 功能套件|[Microsoft SQL Server 2012 SP1 功能套件](https://go.microsoft.com/fwlink/p/?LinkID=268266)中的一個或多個檔案|  
|無 32 位元的 SQL Server 2012 安裝|安裝包括 SP1 的 32 位元 Server 2012 (已預先安裝 SP1 的新執行個體)|SQLServer2012SP1-FullSlipstream-x86-CHT.exe **以及** SQLServer2012SP1-FullSlipstream-x86-CHT.box 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|無 32 位元的 SQL Server 2012 Management Studio 安裝|安裝包括 SP1 的 32 位元 SQL Server 2012 Management Studio|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|無 32 位元版本的 SQL Server 2012 RTM Express|安裝包括 SP1 的 32 位元 SQL Server 2012 Express|SQLEXPR32_x86_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|32 位元的 **SQL Server 2008** 或 **SQL Server 2008 R2**安裝|**就地升級** 為包括 SP1 的 32 位元 SQL Server 2012|SQLServer2012SP1-FullSlipstream-x86-CHT.exe **以及** SQLServer2012SP1-FullSlipstream-x86-CHT.box 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**64 位元安裝：**|||  
|任何 SQL Server 2012 版本的 64 位元版本|升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64 位元版本的 SQL Server 2012 RTM Express|升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 64 位元版本的 SQL Server 2012 SP1|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元版本的 SQL Server 2012 Management Studio Express|升級為 64 位元版本的 SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元版本的任何 SQL Server 2012 版本， **以及** 64 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|[Microsoft SQL Server 2012 RTM 功能套件](https://www.microsoft.com/download/details.aspx?id=44272)中一個或多個 64 位元版本的工具|將工具升級為 64 位元版本的 Microsoft SQL Server 2012 SP1 功能套件|[Microsoft SQL Server 2012 SP1 功能套件](https://go.microsoft.com/fwlink/p/?LinkID=268266)中的一個或多個檔案|  
|無 64 位元的 SQL Server 2012 安裝|安裝包括 SP1 的 64 位元 Server 2012 (已預先安裝 SP1 的新執行個體)|SQLServer2012SP1-FullSlipstream-x64-CHT.exe， **以及** SQLServer2012SP1-FullSlipstream-x64-CHT.box 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|無 64 位元的 SQL Server 2012 Management Studio 安裝|安裝 64 位元的 SQL Server 2012 Management Studio，包括 SP1|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|無 64 位元版本的 SQL Server 2012 RTM Express|安裝 64 位元的 SQL Server 2012 Express，包括 SP1|SQLEXPR_x64_CHT.exe 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元的 **SQL Server 2008** 或 **SQL Server 2008 R2**安裝|**就地升級** 為包括 SP1 的 64 位元 SQL Server 2012|SQLServer2012SP1-FullSlipstream-x64-CHT.exe， **以及** SQLServer2012SP1-FullSlipstream-x64-CHT.box 的下載位置在 [這裡](https://go.microsoft.com/fwlink/p/?LinkID=268158)|  

### <a name="known-issues-fixed-in-this-service-pack"></a>這個 Service Pack 所修正的已知問題  
如需這個 Service Pack 所修正之錯誤和已知問題的完整清單，請參閱 [這份知識庫文件](https://support.microsoft.com/kb/2674319)。   

### <a name="reinstalling--instances-of-sql-server-failover-cluster-fails-if-you-use-the-same-ip-address"></a>如果您使用相同的 IP 位址，重新安裝 SQL Server 容錯移轉叢集的執行個體會失敗  
**問題：** 若在安裝 SQL Server 容錯移轉叢集執行個體時指定了不正確的 IP 位址，安裝就會失敗。 解除安裝失敗的執行個體之後，如果您嘗試使用相同的執行個體名稱和正確的 IP 位址來重新安裝 SQL Server 容錯移轉叢集執行個體，安裝仍會失敗。 發生失敗的原因是先前的安裝遺留了重複的資源群組。  
  
**因應措施：** 若要解決此問題，請在重新安裝時使用不同的執行個體名稱，或在重新安裝之前手動刪除資源群組。 如需詳細資訊，請參閱 [在 SQL Server 容錯移轉叢集中加入或移除節點](failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。 
  
### <a name="analysis-services-and-powerpivot"></a>Analysis Services 和 PowerPivot  
  
##### <a name="powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>PowerPivot 組態工具不會建立 PowerPivot 圖庫  
**問題：** PowerPivot 設定工具會佈建小組網站，因此不會建立 PowerPivot 圖庫。  
  
**因應措施：** 建立新的應用程式 (程式庫)。  
  
1.  確認網站集合功能 **[網站集合的 PowerPivot 功能整合]** 為 [使用中]。  
  
2.  在現有網站的 [網站內容]  頁面中，按一下 [加入應用程式]  。  
  
3.  按一下 [PowerPivot 圖庫]  。  
  
#### <a name="to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>若要使用 PowerPivot for Excel 搭配 Excel 2013，您必須使用與 Excel 一起安裝的增益集  
**問題：** 在 Office 2010 中，PowerPivot for Excel 是可從 [https://www.microsoft.com/bi/powerpivot.aspx](https://www.microsoft.com/bi/powerpivot.aspx) 下載的獨立增益集。 或者，您也可以從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=29074)下載此增益集。 請注意，下載提供兩種版本的 PowerPivot 增益集：其中之一隨附於 SQL Server 2008 R2；另一個則隨附於 SQL Server 2012。 不過，如果是 Office 2013，PowerPivot for Excel 隨附於 Office，而且會在您安裝 Excel 時一併安裝。 雖然 SQL Server 2008 R2 和 SQL Server 2012 版本的 PowerPivot for Excel 2010 與 Excel 2013 不相容，不過如果您想要讓 Excel 2010 與 Excel 2013 並存執行，仍然可以在用戶端電腦上安裝 PowerPivot for Excel 2010。 換言之，這兩種 Excel 版本可以共存，因此對應的 PowerPivot 增益集也可以。  
  
**因應措施：** 若要使用 PowerPivot for Excel 2013，必須啟用 COM 增益集。 在 Excel 2013 中，選取 [檔案]   | [選項]   | [增益集]  。在 [管理]  下拉式方塊中，選取 [COM 增益集]  ，然後按一下 [執行]  。 在 [COM 增益集]  中，選取 [Microsoft Office PowerPivot for Excel 2013]  ，然後按一下 [確定]  。  
  
### <a name="reporting-services"></a>Reporting Services  
  
#### <a name="install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>在安裝 Reporting Services 之前，安裝並設定 SharePoint Server 2013  
**問題：** 安裝 SQL Server Reporting Services (SSRS) **之前**，請先完成下列需求。  
  
1.  執行 SharePoint 2013 產品準備工具。  
  
2.  安裝 SharePoint Server 2013。  
  
3.  執行 SharePoint 2013 產品設定精靈，或完成對等的設定步驟來設定 SharePoint 伺服器陣列。  
  
**因應措施：** 若您在設定 SharePoint 伺服器陣列之前，即已安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式，所要採取的因應措施取決於所安裝的其他元件。  
  
#### <a name="power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>SharePoint Server 2013 中的 Power View 需要使用 Microsoft.AnalysisServices.SPClient.dll  
**問題**：[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不會安裝必要的元件：**Microsoft.AnalysisServices.SPClient.dll**。 如果您在 SharePoint 模式下安裝 SharePoint Server 2013 Preview 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ，但並未下載及安裝 PowerPivot for SharePoint 2013 安裝程式套件 **spPowerPivot.msi** ，則 Power View 將無法運作且會出現下列徵兆。  
  
**徵兆：** 當您嘗試建立 Power View 報表時，會出現類似下列錯誤訊息：  
  
-   「無法與資料來源建立連接...」  
  
內部錯誤詳細資料將會包含類似下面的訊息：  
  
-   「連接字串屬性 'User Identity' 不支援值 'SharePoint Principal'。」  
  
**因應措施：** 在 SharePoint Server 2013 上安裝 PowerPivot for SharePoint 2013 安裝程式套件 (**spPowerPivot.msi**)。 此安裝程式套件屬於 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件的一部分。 您可以從 [!INCLUDE[msCoName](../includes/msconame-md.md)] 下載中心的 [SQL Server 2012 SP1 功能套件](https://go.microsoft.com/fwlink/p/?LinkID=268266)下載此功能套件。  
  
#### <a name="power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>執行已排定的資料重新整理之後，PowerPivot 活頁簿中的 Power View 工作表被刪除  
**問題**：在 PowerPivot for SharePoint 增益集中，如果對含有 Power View 的活頁簿使用 [排定的資料重新整理]  ，將會刪除所有 Power View 工作表。  
  
**因應措施**：若要搭配 Power View 活頁簿使用 [排定的資料重新整理]  ，請建立正好是資料模型的 PowerPivot 活頁簿。 建立含有 Excel 工作表及 Power View 工作表的不同活頁簿，讓這個活頁簿透過資料模型連結至 PowerPivot 活頁簿。 只要針對含有資料模型的 PowerPivot 活頁簿來排程資料重新整理即可。  
  
### <a name="data-quality-services"></a>Data Quality Services  
  
#### <a name="dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>不正確的 SQL Server 2012 版本中提供了 DQS  
**問題：** 在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM 版本中，除了 Enterprise、Business Intelligence 和 Developer Edition 之外的所有 SQL Server 版本，都會提供 Data Quality Services (DQS) 功能。 安裝 SQL Server 2012 SP1 之後，除了 Enterprise、Business Intelligence 和 Developer Edition 以外，所有版本都不再提供 DQS。  
  
**因應措施**：若在不支援的版本中使用 DQS，請升級為支援的版本，或從應用程式中移除這項功能的相依性。  
  
### <a name="sql-server-express"></a>SQL Server Express  
  
#### <a name="full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>SQL Server 2012 Express SP1 提供了完整版本的 SQL Server Management Studio  
SQL Server 2012 Express Service Pack 1 (SP1) 版本包含完整版本的 SQL Server 2012 Management Studio (先前只有 SQL Server 2012 DVD 才提供) 而非 SQL Server 2012 Management Studio Express。 若要下載和安裝 SQL Server 2012 Express SP1，請參閱 [SQL Server 2012 Express Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=267905)。  
  
### <a name="change-data-capture-service-and-designer-for-oracle-by-attunity"></a>Attunity 的 Oracle 異動資料擷取服務和設計工具  
  
#### <a name="upgrading-the-cdc-service-and-designer"></a>升級 CDC 服務和設計工具  
**問題：** 安裝 SQL Server 2012 SP1 時，若電腦上已安裝 Attunity Oracle 異動資料擷取 (CDC) 設計工具和異動資料擷取 (CDC) 服務，這些元件將不會因為安裝 SP1 而升級。  
  
**因應措施：** 若要將 CDC 元件升級為最新版本：  
  
1.  從 [SQL Server 2012 SP1 功能套件下載頁面](https://go.microsoft.com/fwlink/p/?LinkID=268266)下載 Attunity Oracle Change Data Capture (CDC) 服務的 .msi 檔案。  
  
2.  執行 .msi 檔案。  
  
### <a name="sql-server-data-tier-application-framework-dacfx"></a>SQL Server 資料層應用程式架構 (DACFx)  
**就地升級支援**  
  
此版本的資料層應用程式架構 (DACFx) 支援從舊版就地升級，因此不需要在升級至此版本之前移除舊版 DACFx 安裝。 您可以在 [此處](https://msdn.microsoft.com/library/dn702988.aspx)尋找未來的 DACFx 版本。  
  
**支援選擇性 XML 索引**  
  
SQL Server 2012 SP1 加入對 [選擇性 XML 索引 (SXI)](https://msdn.microsoft.com/598ecdcd-084b-4032-81b2-eed6ae9f5d44)的支援，這個新的 SQL Server 功能會提供新的方式來建立提升效能及效率的 XML 資料行資料索引。  
  
DACFx 現在對所有的 DAC 案例及用戶端工具都支援 SXI 索引。 只有在 SSDT 的最新版本才支援 SXI。 SSDT RTM 和 2012 年 9 月版不支援 SXI。  
  
**支援原生 BCP 資料格式**  
  
先前在 DACPAC 及 BACPAC 封裝內部用來儲存資料表資料的資料格式為 JSON。 安裝此更新後，原生 BCP 就會是目前的資料保存格式。 這項變更可將提升的 SQL Server 資料類型精確度引入 DACFx，包括支援 SQL_Variant 類型，以及增強大規模資料庫的資料部署效能。  
  
**在整個套件建立/部署中保留 CHECK 條件約束狀態**  
  
DACFx 先前並不能將資料表上定義的檢查條件約束狀態 (WITH CHECK/NOCHECK) 保留在資料庫結構描述中，也無法將此資訊儲存在 DACPAC 內部。 當有違反檢查條件約束的資料表資料存在時，此行為可能會在封裝部署上產生潛在問題。 安裝此更新後，DACFx 現在從資料庫中擷取檢查條件約束的目前狀態時，就會將此狀態儲存在 DACPAC 中，並於部署封裝時適當還原該狀態。  
  
**SqlPackage.exe (DACFx 命令列工具) 的更新**  
  
-   擷取包含資料的 DACPAC - 從即時 SQL Server 或 Azure SQL Database 建立資料庫快照集檔案 (.dacpac)，不僅包含資料庫結構描述，還包含使用者資料表中的資料。 您可以使用 SqlPackage.exe 發佈動作將這些套件發行至新的或現有 SQL Server 或 Azure SQL Database。 封裝中的資料將會取代目標資料庫中的現有資料。  
  
-   匯出 BACPAC - 建立即時 SQL Server 或 Azure SQL Database 的邏輯備份檔案 (.bacpac)，內含資料庫結構描述，以及可用於將資料庫從內部部署 SQL Server 移轉至 Azure SQL Database 的使用者資料。 您可以匯出與 Azure 相容的資料庫，稍後再於支援的 SQL Server 版本之間將其匯入。  
  
-   匯入 BACPAC - 匯入 .bacpac 檔案以全新建立或填入空的 SQL Server 或 Azure SQL Database。  
  
MSDN 上的完整 SqlPackage.exe 文件可以在 [此處](https://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)找到。  
  
**套件相容性**  
  
此版本導入數個適用於 DAC 封裝的向前相容性。  
  
-   此版本所建立未包含 SXI 元素或資料表資料的 DAC 封裝可供舊版 DACFx (SQL Server 2012 RTM、SQL Server 2012 CU1 和 DACFx 2012 年 9 月版) 取用。  
  
-   此版本可以使用舊版 DACFx 建立的所有 DAC 封裝。  
  
## <a name="see-also"></a>另請參閱
- [安裝 SQL Server 2012 服務更新](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [如何識別 SQL Server 版本與版本類型](https://support.microsoft.com/help/321185)
- [安裝 SQL Server 2012 服務更新](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [如何識別 SQL Server 版本與版本類型](https://support.microsoft.com/help/321185) 
- [如何判斷 SQL Server 的版本](https://support.microsoft.com/kb/321185)  
- [SQL Server 2014 各版本所支援的功能](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
