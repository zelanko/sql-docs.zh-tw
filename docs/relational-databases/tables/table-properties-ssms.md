---
title: "資料表屬性 - SSMS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.tableproperties.storage.f1
- sql13.swb.tableproperties.changetracking.f1
- sql13.swb.tableproperties.general.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql13.swb.tableproperties.filetable.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 077c29bc7c18f6b48d4ff336fb59a32fe28390d9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="table-properties---ssms"></a>Table Properties - SSMS
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  本主題描述在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]之 [資料表屬性] 對話方塊中顯示的資料表屬性。 如需如何顯示這些屬性的詳細資訊，請參閱 [檢視資料表定義](../../relational-databases/tables/view-the-table-definition.md)。  
  
 **本主題內容**  
  
1.  [一般頁面](#GeneralPage)  
  
2.  [變更追蹤頁面](#ChangeTracking)  
  
3.  [FileTable 頁面](#FileTable)  
  
4.  [儲存體頁面](#Storage)  
  
##  <a name="GeneralPage"></a> 一般頁面  
 **資料庫**  
 包含此資料表之資料庫的名稱。  
  
 **Server**  
 目前伺服器執行個體的名稱。  
  
 **使用者**  
 這個連接之使用者的名稱。  
  
 **建立日期**  
 資料表的建立日期和時間。  
  
 **名稱**  
 資料表的名稱。  
  
 **結構描述**  
 擁有資料表的結構描述。  
  
 **系統物件**  
 指出此資料表是系統資料表，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來包含內部資訊。 使用者不應該直接變更或參考系統資料表。  
  
 **ANSI NULLS**  
 指出物件是否使用設定為 ON 的 ANSI NULLS 選項建立。 如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)。  
  
 **引號識別碼**  
 指出物件是否使用設定為 ON 的引號識別碼選項建立。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)。  
  
 **鎖定擴大**  
 表示資料表的鎖定擴大資料粒度。 如需有關 Database Engine 中鎖定的詳細資訊，請參閱 [SQL Server 交易鎖定與資料列版本設定指南](http://msdn.microsoft.com/library/jj856598.aspx)。 可能的值為：  
  
 AUTO  
 此選項允許 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 選取適用於資料表結構描述的鎖定擴大資料粒度。  
  
-   如果資料表為資料分割，則允許鎖定擴大使用堆積或 B 型樹狀結構 (HoBT) 資料粒度。 鎖定在擴大為 HoBT 層級後，就無法再擴大為 TABLE 資料粒度。  
  
-   如果資料表不是分割區，則會對 TABLE 資料粒度執行鎖定擴大。  
  
 TABLE  
 不論資料表是否為資料分割，鎖定擴大將在資料表層級的資料粒度完成。 TABLE 為預設值。  
  
 DISABLE  
 在大多數情況下都避免使用鎖定擴大， 但並非完全不允許資料表層級的鎖定。 例如，當您在可序列化隔離層級下掃描沒有任何叢集索引的資料表時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須採用資料表鎖定以保護資料的完整性。  
  
 **資料表有複寫**  
 指出何時使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫，將資料表複寫到另一個資料庫。 可能的值為 **True** 或 **False**。  
  
##  <a name="ChangeTracking"></a> 變更追蹤頁面  
 **變更追蹤**  
 指出資料表是否啟用變更追蹤。 預設值為 **[False]**。  
  
 只有當資料庫啟用了變更追蹤時，才能使用此選項。  
  
 若要啟用變更追蹤，資料表必須具有主索引鍵，而您也必須擁有修改資料表的權限。 您可以使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)來設定變更追蹤。  
  
 **追蹤資料行已更新**  
 指出 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 是否追蹤哪些資料行已更新。  
  
 如需變更追蹤的詳細資訊，請參閱[關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)。  
  
##  <a name="FileTable"></a> FileTable 頁面  
 顯示與 FileTable 相關之資料表的屬性。 如需詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。  
  
 **FileTable 名稱資料行定序**  
 要套用至 FileTable 中 **Name** 資料行的定序。 **Name** 資料行包含檔案和目錄名稱。  
  
 **FileTable 目錄名稱**  
 FileTable 的根資料夾。  
  
 **已啟用 FileTable 命名空間**  
 當為 **True**時，這個值表示資料表為 FileTable。 如果您將這個值變更為 **False**，您會將 FileTable 變更為一般使用者資料表。 如果您之後想要將資料表變更回 FileTable，此資料表必須先通過 FileTable 一致性檢查才會轉換成功。  
  
##  <a name="Storage"></a> 儲存體頁面  
 顯示選取之資料表的儲存體相關屬性。  
  
### <a name="compression"></a>壓縮  
 **壓縮類型**  
 資料表的壓縮類型。 此屬性只適用於沒有資料分割的資料表。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。  
  
 **使用頁面壓縮的資料分割**  
 使用頁面壓縮的資料分割數。 此屬性只適用於資料分割的資料表。  
  
 **未壓縮的資料分割**  
 未壓縮的資料分割數。 此屬性只適用於資料分割的資料表。  
  
 **使用資料列壓縮的資料分割**  
 使用資料列壓縮的資料分割數。 此屬性只適用於資料分割的資料表。  
  
### <a name="filegroup"></a>檔案群組  
 **文字檔案群組**  
 包含資料表文字資料之檔案群組的名稱。  
  
 **檔案群組**  
 資料表所在的檔案群組的名稱。  
  
 **資料表已經分割**  
 可能的值為 **True** 和 **False**。  
  
 **檔案資料流檔案群組**  
 如果資料表擁有具有 FILESTREAM 屬性的 **varbinary(max)** 資料行，則指定 FILESTREAM 資料檔案群組的名稱。 預設值為預設的 FILESTREAM 資料檔案群組。  
  
 如果資料表不包含 FILESTREAM 資料，則此欄位空白。  
  
### <a name="general"></a>一般  
 **Vardecimal 儲存格式已啟用**  
 如果是 **True**，這個唯讀值表示 **decimal** 和 **numeric** 資料類型會使用 vardecimal 儲存格式來儲存。 若要變更這個選項，請使用 **sp_tableoption** 的 [vardecimal storage format](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)選項。 Vardecimal 儲存格式已被取代。 請改用資料列壓縮。  
  
 **索引空間**  
 顯示索引在資料表中所佔的空間量 (以 MB 表示)。 這個值不包括資料表的 XML 索引空間使用量。 如果 XML 索引屬於此資料表，請改用 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 。  
  
 **資料列計數**  
 資料表中的資料列數。  
  
 **資料空間**  
 資料在資料表中所佔的空間量 (以 MB 表示)。  
  
### <a name="partitioning"></a>資料分割  
 只有在資料表為資料分割時，才能使用此區段。 如需詳細資訊，請參閱 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 **資料分割資料行**  
 用以分割資料表之資料行的名稱。  
  
 **分割區配置**  
 如果資料表為資料分割，則為資料分割配置的名稱。 如果資料表不是資料分割，則此欄位空白。  
  
 **資料分割數目**  
 資料表中的資料分割數。  
  
 **FILESTREAM 資料分割配置**  
 如果資料表為資料分割，則為 FILESTREAM 資料分割配置的名稱。 如果資料表不是資料分割，則此欄位空白。  
  
 FILESTREAM 資料分割配置必須對稱於在 **[資料分割配置]** 選項中所指定的配置。  
  
## <a name="see-also"></a>另請參閱  
 [檢視資料表定義](../../relational-databases/tables/view-the-table-definition.md)   
 [修改資料行 &#40;Database Engine&#41;](../../relational-databases/tables/modify-columns-database-engine.md)  
  
  
