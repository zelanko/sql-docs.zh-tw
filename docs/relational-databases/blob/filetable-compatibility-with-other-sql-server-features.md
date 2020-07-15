---
title: FileTable 相容性 | Microsoft Docs
description: 了解 FileTable 與其他 SQL Server 功能搭配運作的方式。 閱讀 SQL Server 針對 FileTable 支援的功能，以及其施行的條件約束。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a1899aefaeeef896112a903f1fe69b289740ef09
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85642559"
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>FileTable 與其他 SQL Server 功能的相容性
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  描述 FileTable 如何搭配其他的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能一起運作。  
  
##  <a name="alwayson-availability-groups-and-filetables"></a><a name="alwayson"></a> AlwaysOn 可用性群組和 FileTable  
 當包含 FILESTREAM 或 FileTable 資料的資料庫屬於 AlwaysOn 可用性群組時：  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]僅部分支援 FileTable 功能。 在容錯移轉之後，主要複本上的 FileTable 資料可供存取，但卻無法存取位在可讀取之次要複本上的 FileTable 資料。  
  
    > **注意：** 請注意，容錯移轉後將支援所有 FILESTREAM 功能。 可讀取的次要複本以及新的主要複本上的 FILESTREAM 資料皆可供存取。  
  
-   FILESTREAM 和 FileTable 函數會接受或傳回虛擬網路名稱 (VNN) 而非電腦名稱。 如需有關這些函數的詳細資訊，請參閱 [Filestream and FileTable Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md) (Filestream 和 FileTable 函數 (Transact-SQL))。  
  
-   透過檔案系統 API 對 FILESTREAM 或 FileTable 資料進行的所有存取都應該使用 VNN 而非電腦名稱。 如需詳細資訊，請參閱 [FILESTREAM 和 FileTable 與 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
##  <a name="partitioning-and-filetables"></a><a name="OtherPartitioning"></a> 資料分割和 FileTable  
 FileTable 不支援資料分割。 有了多重 FILESTREAM 檔案群組的支援，在大多數情況下可以處理單純的向上擴充問題，而不必訴諸於資料分割 (不同於 SQL 2008 FILESTREAM)。  
  
##  <a name="replication-and-filetables"></a><a name="OtherRepl"></a> 複寫和 FileTable  
 FileTable 不支援複寫和相關功能 (包括異動複寫、合併式複寫、異動資料擷取和變更追蹤)。  
  
##  <a name="transaction-semantics-and-filetables"></a><a name="OtherIsolation"></a> 交易語意和 FileTable  
 **Windows 應用程式**  
 Windows 應用程式不了解資料庫交易，所以 Windows 寫入作業不會提供資料庫交易的 ACID 屬性。 因此，交易式回復和復原無法利用 Windows 更新作業來進行。  
  
 **Transact-SQL 應用程式**  
 對於在 FileTable 的 FILESTREAM (file_stream) 資料行中工作的 TSQL 應用程式而言，隔離語意與一般使用者資料表內的 FILESTREAM 資料類型相同。  
  
##  <a name="query-notifications-and-filetables"></a><a name="OtherQueryNot"></a> 查詢通知和 FileTable  
 此查詢不得在 WHERE 子句或是查詢的任何其他部分中，包含 FileTable 中 FILESTREAM 資料行的參考。  
  
##  <a name="select-into-and-filetables"></a><a name="OtherSelectInto"></a> SELECT INTO 和 FileTable  
 FileTable 中的 SELECT INTO 陳述式將不會傳播目的地資料表上所建立的 FileTable 語意 (就像一般資料表中的 FILESTREAM 資料行一樣)。 所有目的地資料表資料行的行為就像一般資料行一樣。 這些資料行不會有任何關聯的 FileTable 語意。  
  
##  <a name="triggers-and-filetables"></a><a name="OtherTriggers"></a> 觸發程序和 FileTable  
 **DDL (資料定義語言) 觸發程序**  
 包含 FileTable 的 DDL 觸發程序並無特殊考量。 一般 DDL 觸發程序將針對 Create/Alter DATABASE 作業以及 FileTable 的 CREATE/ALTER TABLE 作業引發。 觸發程序可以透過呼叫 EVENTDATA() 函數，擷取實際事件資料，該資料包括 DDL 命令文字和其他資訊。 現有 Eventdata 結構描述沒有任何新的事件或變更。  
  
 **DML (資料操作語言) 觸發程序**  
 在建立觸發程序的 DDL 作業期間將會強制施行這些限制。  
  
-   FileTable 將不會支援 DML 作業的 INSTEAD OF 觸發程序。 包含 FILESTREAM 資料行的所有資料表都有現有的限制。  
  
-   FileTable 將會支援 DML 作業的 AFTER 觸發程序。  
  
-   FileTable 上定義的觸發程序無法更新任何 FileTable (包括父系 FileTable)。 這項限制存在的目的主要是為了避免觸發程序與相同交易中檔案系統存取所持有的鎖定之間發生鎖定衝突。  
  
 **非交易式存取以及它對觸發程序的影響**  
 -   當某個資料庫允許非交易式更新存取時，您就可以針對任何資料表中的 FILESTREAM 資料進行就地更新，包括該資料庫中的 FileTable。 由於這種可能性，因此觸發程序可能無法使用 FILESTREAM 內容的前置資料影像。  
  
-   如果是透過檔案系統的非交易式更新作業，SQL Server 將會建立內部交易來擷取 CloseHandle 作業，而且任何已定義的 DML 觸發程序可能會當做該交易的一部分引發。 雖然無法防止觸發程序主體內部之這類交易的回復，不過這項作業不會回復已對 FILESTREAM 所做的變更。  這類回復可能也會防止系統引發 Update 觸發程序，即使 FILESTREAM 內容可能已經變更也一樣。  
  
-   除了這些影響以外，FileTable 的觸發程序也需要處理其他幾個行為  
  
    -   如果是透過檔案系統針對 FileTable 進行的非交易式更新作業，FILESTREAM 內容可能會由其他 Win32 作業獨佔鎖定，而且可能無法透過觸發程序主體進行讀取/寫入存取。 在這類情況中，任何嘗試存取觸發程序主體中之 FILESTREAM 內容的行為都可能會產生「共用違規」錯誤。 因此，觸發程序應該設計成可正確處理這類錯誤。  
  
    -   FILESTREAM 的 AFTER 影像可能不穩定，因為在某些情況下，其他非交易式更新可能基於檔案系統存取所允許的共用模式，同時主動寫入該影像。  
  
-   不正常終止 Win32 控制代碼 (例如管理員明確終止 Win32 控制代碼或是資料庫損毀) 將不會在復原作業期間執行使用者觸發程序，即使不正常終止的 Win32 應用程式可能已經變更 FILESTREAM 內容也是一樣。  
  
##  <a name="views-and-filetables"></a><a name="OtherViews"></a> 檢視表和 FileTable  
 **檢視**  
 可以在 FileTable 上建立檢視表，就像在任何其他資料表上建立一樣。 但是，在 FileTable 上建立的檢視表要考量以下事項：  
  
-   檢視表將不會有任何 FileTable 語意。 例如，檢視表中的資料行 (包括 [檔案屬性] 資料行) 的行為就像一般檢視表資料行一樣，沒有任何特殊的語意，代表檔案/目錄的資料列也是相同情形。  
  
-   檢視表可能會依據「可更新的檢視表」語意來更新，但是基礎資料表條件約束可以拒絕更新，就像在資料表中一樣。  
  
-   檔案的檔案路徑可以在檢視表中視覺化，其方式是將它新增為檢視表中的明確資料行。 例如：  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, ..., GetFileNamespacePath() AS PATH, column3,...  FROM Documents`  
  
 **索引檢視表**  
 目前的索引檢視表不得包含 FILESTREAM 資料行，或是相依於 FILESTREAM 資料行的計算資料行/保存的計算資料行。 當 FileTable 上定義檢視表時，這個行為依然不會變更。  
  
##  <a name="snapshot-isolation-and-filetables"></a><a name="OtherSnapshots"></a> 快照集隔離和 FileTable  
 Read Committed 快照集隔離 (RCSI) 和快照集隔離 (SI) 會依賴擁有資料快照集可供讀取者使用的能力，即使資料上發生更新作業也是一樣。 但是，FileTables 允許對 Filestream 資料的非交易式寫入存取。 因此，以下限制適用於在包含 FileTable 的資料庫中使用這些功能：  
  
-   可以更改包含 FileTable 的資料庫來啟用 RCSI/SI。  
  
-   當資料庫的非交易式存取設定為 FULL 時，在 RCSI 或 SI 之下執行的交易具有以下行為：  
  
    -   讀取到 FileTable file_stream 資料行的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 都會失敗。 資料行的 INSERT 和 UPDATE 依然會成功，只要不是從 file_stream 資料行讀取。  
  
    -   如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式指定 READCOMMITTEDLOCK 資料表提示，讀取將會成功，而且將會取得資料列的鎖定，而不是使用資料列版本設定。  
  
    -   交易 Win32 FileStream 開啟要求也會失敗。  
  
    -   非交易 FileTable Win32 存取會成功。 FileTable 執行的所有內部查詢都不會受到影響。  
  
    -   全文檢索索引一定會成功，不論資料庫選項為何 (READ_COMMITTED_SNAPSHOT 或 ALLOW_SNAPSHOT_ISOLATION)。  
  
##  <a name="readable-secondary-databases"></a><a name="readsec"></a> 可讀取次要資料庫  
 快照集的相同考量，如上節＜ [快照集隔離和 FileTable](#OtherSnapshots)＞所述，也適用於可讀取次要資料庫。  
  
##  <a name="contained-databases-and-filetables"></a><a name="CDB"></a> 自主資料庫和 FileTable  
 FileTable 功能相依的 FILESTREAM 功能必須先在資料庫外部進行一些設定。 因此，使用 FILESTREAM 或 FileTable 的資料庫並非完全自主。  
  
 若要使用自主資料庫的特定功能 (例如包含的使用者)，可以將資料庫內含項目設定為 PARTIAL。 但在此情況下，必須注意某些資料庫設定不會包含在資料庫中，因此不會隨資料庫移動自動移動。  
  
## <a name="see-also"></a>另請參閱  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
