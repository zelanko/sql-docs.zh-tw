---
title: FILESTREAM 與其他 SQL Server 功能的相容性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb904d5e7c0804f4c0f9c84936bb3099c86e28be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923003"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>FILESTREAM 與其他 SQL Server 功能的相容性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  由於 FILESTREAM 資料位於檔案系統中，所以本主題提供了搭配下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能使用 FILESTREAM 的一些考量、指導方針和限制：  
  
-   [SQL Server Integration Services (SSIS)](#ssis)  
  
-   [分散式查詢和連結的伺服器](#distqueries)  
  
-   [加密](#encryption)  
  
-   [資料庫快照集](#DatabaseSnapshot)  
  
-   [複寫](#Replication)  
  
-   [記錄傳送](#LogShipping)  
  
-   [資料庫鏡像](#DatabaseMirroring)  
  
-   [全文檢索索引](#FullText)  
  
-   [容錯移轉叢集](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [自主資料庫](#contained)  
  
##  <a name="ssis"></a> SQL Server Integration Services (SSIS)  
 SQL Server Integration Services (SSIS) 會使用 DT_IMAGE SSIS 資料類型來處理資料流程中的 FILESTREAM 資料，就像處理任何其他 BLOB 資料一樣。  
  
 您可以使用匯入資料行轉換，將檔案系統中的檔案載入 FILESTREAM 資料行中。 您也可以使用匯出資料行轉換，將檔案從 FILESTREAM 資料行擷取至檔案系統中的其他位置。  
  
##  <a name="distqueries"></a> 分散式查詢和連結的伺服器  
 可透過分散式查詢和連結的伺服器，將 FILESTREAM 資料當作 **varbinary(max)** 資料來使用。 在使用四部分名稱的分散式查詢中，即使此名稱參考本機伺服器，也無法使用 FILESTREAM **PathName()** 函數。 不過， **PathName()** 可在使用 **OPENQUERY()** 之傳遞查詢的內部查詢中使用。  
  
##  <a name="encryption"></a> 加密  
 即使啟用了透明資料加密，FILESTREAM 資料也不會加密。  
  
##  <a name="DatabaseSnapshot"></a> 資料庫快照集  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援將 [資料庫快照集](../../relational-databases/databases/database-snapshots-sql-server.md) 用於 FILESTREAM 檔案群組。 如果 FILESTREAM 檔案群組包含在 CREATE DATABASE ON 子句中，此陳述式將會失敗，並引發錯誤。  
  
 當您使用 FILESTREAM 時，可以建立標準 (非 FILESTREAM) 檔案群組的資料庫快照集。 FILESTREAM 檔案群組將會針對這些資料庫快照集標示為離線。  
  
 在資料庫快照集中，FILESTREAM 資料表上執行的 SELECT 陳述式不能包含 FILESTREAM 資料行，否則會傳回下列錯誤訊息：  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> 複寫  
 在簽發者上啟用 FILESTREAM 屬性的 **varbinary(max)** 資料行可以複寫到訂閱者上 (不論有沒有 FILESTREAM 屬性)。 若要指定複寫資料行的方式，請使用 [發行項屬性 - \<發行項>] 對話方塊或是 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 或 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 的 @schema_option 參數。 複寫到沒有 FILESTREAM 屬性之 **varbinary(max)** 資料行的資料不能超過該資料類型的 2-GB 限制，否則會產生執行階段錯誤。 我們建議您最好複寫 FILESTREAM 屬性，除非您要將資料複寫到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 不論所指定的結構描述選項為何，目前皆不支援將含有 FILESTREAM 資料行的資料表複寫至 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 訂閱者。  
  
> [!NOTE]  
>  將大型資料值從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 複寫到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 訂閱者受到最大 256 MB 資料值的限制。 如需詳細資訊，請參閱＜ [SQL Server 2005 的最大容量規格](http://go.microsoft.com/fwlink/?LinkId=103810)＞。  
  
### <a name="considerations-for-transactional-replication"></a>異動複寫考量  
 如果您在針對異動複寫發行之資料表中使用 FILESTREAM 資料行，請注意以下考量：  
  
-   如果有任何資料表包含具有 FILESTREAM 屬性 (attribute) 的資料行，您將無法針對 [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 的 @sync_method 屬性 (property) 使用「資料庫快照集」或「資料庫快照集字元」的值。  
  
-   max text repl size 選項會指定可以插入要發行以供複寫之資料行中的資料數量上限。 此選項可用來控制所複寫之 FILESTREAM 資料的大小。  
  
-   如果您指定此結構描述選項來複寫 FILESTREAM 屬性，但是您篩選出 FILESTREAM 所需的 **uniqueidentifier** 資料行，或是指定不要為此資料行複寫 UNIQUE 條件約束，則複寫作業不會複寫 FILESTREAM 屬性。 此資料行只會複寫為 **varbinary(max)** 資料行。  
  
### <a name="considerations-for-merge-replication"></a>合併式複寫考量  
 如果您在針對合併式複寫發行之資料表中使用 FILESTREAM 資料行，請注意以下考量：  
  
-   合併式複寫和 FILESTREAM 都需要 **uniqueidentifier** 資料類型的資料行，以識別資料表中的每一個資料列。 如果資料表沒有資料行，合併式複寫會自動加入資料行。 合併式複寫會要求此資料行設定 ROWGUIDCOL 屬性及具有 NEWID() 或 NEWSEQUENTIALID() 的預設值。 除了這些需求以外，FILESTREAM 也要求必須針對此資料行定義 UNIQUE 條件約束。 這些需求的結果如下：  
  
    -   如果您將 FILESTREAM 資料行加入至已針對合併式複寫發行的資料表中，請確定 **uniqueidentifier** 資料行具有 UNIQUE 條件約束。 如果它沒有 UNIQUE 條件約束，請將具名條件約束加入至發行集資料庫內的資料表。 根據預設，合併式複寫將會發行這個結構描述變更，並將此變更套用到每一個訂閱資料庫。  
  
         如果您如所述的內容手動加入 UNIQUE 條件約束，而且您想要移除合併式複寫，您就必須先移除 UNIQUE 條件約束，否則複寫移除將會失敗。  
  
    -   根據預設，合併式複寫會使用 NEWSEQUENTIALID()，因為它可以提供比 NEWID() 更好的效能。 如果您將 **uniqueidentifier** 資料行加入將針對合併式複寫發行的資料表中，請將 NEWSEQUENTIALID() 指定為預設值。  
  
-   合併式複寫包括複寫大型物件類型的最佳化， 此最佳化作業是由 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 的 @stream_blob_columns 參數所控制。 如果您設定此結構描述選項來複寫 FILESTREAM 屬性，則 @stream_blob_columns 參數值會設定為 **true**。 可以使用 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)來覆寫此最佳化。 這個預存程序可讓您將 @stream_blob_columns 設定為 **false**。 如果您將 FILESTREAM 資料行加入至已針對合併式複寫發行的資料表中，我們建議您使用 sp_changemergearticle 將此選項設定為 **true** 。  
  
-   如果 FILESTREAM 資料行中的資料超過 2 GB，而且複寫之後發生了衝突，則在建立發行項之後針對 FILESTREAM 啟用此結構描述選項會造成複寫失敗。 如果您預期會發生這個狀況，建議您卸除及重新建立資料表發行項，並在建立時啟用適當的 FILESTREAM 結構描述選項。  
  
-   合併式複寫可以透過 HTTPS 連接同步處理 FILESTREAM 資料 (利用 [Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md))。 這項資料不能超過 Web 同步處理的 50 MB 限制，否則會產生執行階段錯誤。  
  
##  <a name="LogShipping"></a> 記錄傳送  
 [記錄傳送](../../database-engine/log-shipping/about-log-shipping-sql-server.md) 支援 FILESTREAM。 主要和次要伺服器都必須執行 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]或更新的版本，並啟用 FILESTREAM。  
  
##  <a name="DatabaseMirroring"></a> 資料庫鏡像  
 資料庫鏡像不支援 FILESTREAM。 不能在主體伺服器上建立 FILESTREAM 檔案群組。 不能針對包含 FILESTREAM 檔案群組的資料庫設定資料庫鏡像。  
  
##  <a name="FullText"></a> 全文檢索索引  
 [全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md) 處理 FILESTREAM 資料行的方式，與處理 **varbinary(max)** 資料行的方式相同。 FILESTREAM 資料表必須有一個資料行包含每一個 FILESTREAM BLOB 的副檔名。 如需詳細資訊，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)、[設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)和 [sys.fulltext_document_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)。  
  
 全文檢索引擎會針對 FILESTREAM BLOB 的內容建立索引。 為檔案 (如影像) 建立索引可能不會很實用。 當更新 FILESTREAM BLOB 時，會為它重新建立索引。  
  
##  <a name="FailoverClustering"></a> 容錯移轉叢集  
 當您進行容錯移轉叢集時，FILESTREAM 檔案群組必須放在共用磁碟上。 FILESTREAM 必須在叢集中主控 FILESTREAM 執行個體的每一個節點上啟用。 如需詳細資訊，請參閱 [設定容錯移轉叢集上的 FILESTREAM](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)。  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 支援 FILESTREAM。 10-GB 的資料庫大小限制不包括 FILESTREAM 資料容器。  
  
##  <a name="contained"></a> 自主資料庫  
 FILESTREAM 功能必須先在資料庫外部進行一些設定。 因此，使用 FILESTREAM 或 FileTable 的資料庫並非完全自主。  
  
 若要使用自主資料庫的特定功能 (例如包含的使用者)，可以將資料庫內含項目設定為 PARTIAL。 但在此情況下，必須注意某些資料庫設定不會包含在資料庫中，因此不會隨資料庫移動自動移動。  
  
## <a name="see-also"></a>另請參閱  
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
