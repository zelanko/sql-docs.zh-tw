---
title: 執行大量複製作業
description: 了解使用 OLE DB Driver for SQL Server 執行大量複製作業，以及其如何讓資料快速傳輸到資料庫中。
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- bulk copy [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], bulk copy operations
- OLE DB Driver for SQL Server, bulk copy operations
- MSOLEDBSQL, bulk copy operations
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6035f5ac8723e9ccb84735080569468c1b7b33b3
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123848"
---
# <a name="performing-bulk-copy-operations"></a>執行大量複製作業
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製功能支援將大量資料傳送進出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表或檢視。 資料也可以藉由指定 SELECT 陳述式而向外傳送。 您可在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和作業系統資料檔 (例如 ASCII 檔) 之間移動。 資料檔可能具有不同的格式；您可將格式定義為以格式檔來大量複製。 或者，也可以使用大量複製函數和方法，將資料載入程式變數，然後傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 如需示範此功能的範例應用程式，請參閱[使用 IRowsetFastLoad 大量複製資料 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)。  
  
 應用程式通常會以下列其中一種方式使用大量複製：  
  
-   從資料表、檢視或 Transact-SQL 陳述式的結果集大量複製到資料檔，其中資料會以與資料表或檢視相同的格式儲存。  
  
     這稱為原生模式的資料檔案。  
  
-   從資料表、檢視或 Transact-SQL 陳述式的結果集大量複製到資料檔，其中儲存資料的格式會與資料表或檢視不同。  
  
     在此情況下，會在每一個資料行儲存到資料檔中時，為其建立另一個定義特性 (資料類型、位置、長度、結束字元等) 的格式檔案。 如果所有的資料行都轉換成字元格式，則產生的檔案稱為字元模式資料檔。  
  
-   從資料檔大量複製到資料表或檢視。  
  
     如有需要，可使用格式檔來判斷資料檔的配置。  
  
-   將資料載入程式變數，然後使用可在資料行中一次複製大量資料的大量複製函數，將資料匯入資料表或檢視。  
  
 大量複製函數所使用的資料檔不必由其他的大量複製程式建立。 任何其他的系統都可以根據大量複製定義產生資料檔和格式檔；之後可以將這些檔案搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製程式使用，以將資料匯入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 例如，您可以從試算表將資料匯出至 Tab 鍵分隔檔案、建立描述 Tab 鍵分隔檔案的格式檔，然後使用大量複製程式將資料快速匯入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 大量複製所產生的資料檔也可以匯入至其他應用程式。 例如，您可以使用大量複製函數，將資料從資料表或檢視匯出至 Tab 鍵分隔檔案，然後再將該檔案載入至試算表。  
  
 程式設計人員在撰寫使用大量複製函數的應用程式時，應該遵照大量複製良好效能的一般規則。 如需有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中大量複製作業支援的詳細資訊，請參閱[資料的大量匯入及匯出 &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 CLR 使用者定義型別 (UDT) 必須繫結為二進位資料。 即使格式檔指定 SQLCHAR 做為目標 UDT 資料行的資料類型，BCP 公用程式也會將該資料視為二進位。  
  
 請勿將 SET FMTONLY OFF 用於大量複製作業。 SET FMTONLY OFF 可能會導致大量複製作業失敗或提供未預期的結果。  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 OLE DB Driver for SQL Server 會實作兩個方法，以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫執行大量複製作業。 第一個方法涉及使用 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 介面進行以記憶體為基礎的大量複製作業；第二個方法則涉及使用 [IBCPSession](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md) 介面進行以檔案為基礎的大量複製作業。  
  
### <a name="using-memory-based-bulk-copy-operations"></a>使用以記憶體為基礎的大量複製作業  
 OLE DB Driver for SQL Server 實作 **IRowsetFastLoad** 介面，以公開對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以記憶體為基礎之大量複製作業的支援。 **IRowsetFastLoad** 介面會實作 [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) 和 [IRowsetFastLoad::InsertRow](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) 方法。  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>針對 IRowsetFastLoad 啟用工作階段  
 取用者會將其大量複製的需求通知 OLE DB Driver for SQL Server，方法是，將 OLE DB Driver for SQL Server 特有的資料來源屬性 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE。 在資料來源上設定該屬性後，取用者會建立 OLE DB Driver for SQL Server 工作階段。 新的工作階段可以讓取用者存取 **IRowsetFastLoad** 介面。  
  
> [!NOTE]  
>  如果使用 **IDataInitialize** 介面來初始化資料來源，則必須在 **IOpenRowset::OpenRowset** 方法的 *rgPropertySets* 參數中設定 SSPROP_IRowsetFastLoad 屬性，否則對 **OpenRowset** 方法的呼叫將傳回 E_NOINTERFACE。  
  
 針對大量複製而啟用工作階段，會限制 OLE DB Driver for SQL Server 對該工作階段上介面的支援。 啟用大量複製功能的工作階段只會公開下列介面：  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 若要停止建立啟用大量複製功能的資料列集，並導致 OLE DB Driver for SQL Server 工作階段還原為標準處理，請將 SSPROP_ENABLEFASTLOAD 重設為 VARIANT_FALSE。  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad Rowsets  
 OLE DB Driver for SQL Server 大量複製資料列集是唯寫的，但會公開介面讓取用者得以判斷 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表的結構。 下列介面會在啟用大量複製功能的 OLE DB Driver for SQL Server 資料列集上公開：  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 提供者特定的屬性 SSPROP_FASTLOADOPTIONS、SSPROP_FASTLOADKEEPNULLS 和 SSPROP_FASTLOADKEEPIDENTITY 可控制 OLE DB Driver for SQL Server 大量複製資料列集的行為。 這些屬性是在 *rgPropertySets* **IOpenRowset** 參數成員的 *rgProperties* 成員中指定的。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|資料行：否<br /><br /> R/W︰讀取/寫入<br /><br /> 輸入：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：維護取用者所提供的識別值。<br /><br /> VARIANT_FALSE：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中識別資料行的值是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 產生。 OLE DB Driver for SQL Server 會忽略為資料行所繫結的任何值。<br /><br /> VARIANT_TRUE：取用者會繫結為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別資料行提供值的存取子。 在接受 NULL 的資料行上不提供識別屬性，所以取用者會在每個 **IRowsetFastLoad::Insert** 呼叫上提供唯一值。|  
|SSPROP_FASTLOADKEEPNULLS|資料行：否<br /><br /> R/W︰讀取/寫入<br /><br /> 輸入：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：針對具有 DEFAULT 條件約束的資料行維護 NULL。 只對接受 NULL 且套用 DEFAULT 條件約束的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行造成影響。<br /><br /> VARIANT_FALSE：當 OLE DB Driver for SQL Server 取用者插入的資料列包含資料行要用的 NULL 時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會插入資料行的預設值。<br /><br /> VARIANT_TRUE：當 OLE DB Driver for SQL Server 取用者插入的資料列包含資料行要用的 NULL 時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會插入 NULL 作為資料行值。|  
|SSPROP_FASTLOADOPTIONS|資料行：否<br /><br /> R/W︰讀取/寫入<br /><br /> 輸入：VT_BSTR<br /><br /> 預設值：無<br /><br /> 描述：這個屬性與 **bcp** 公用程式的 **-h** "*hint*[,...*n*]" 選項相同。 將資料大量複製到資料表時，可使用下列字串做為選項。<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,...*n*]):資料檔案中資料的排序次序。 如果載入的資料檔是依照資料表的叢集索引來排序，將可增進大量複製的效能。<br /><br /> **ROWS_PER_BATCH** = *bb*：每一批資料的資料列數目 (如 *bb*)。 伺服器根據 *bb* 值，將大量載入最佳化。 根據預設，**ROWS_PER_BATCH** 是未知的。<br /><br /> **KILOBYTES_PER_BATCH** = *cc*：每一批資料的 KB 數目 (如 cc)。 根據預設，**KILOBYTES_PER_BATCH** 是未知的。<br /><br /> **TABLOCK**：在大量複製作業期間必須使用資料表層級鎖定。 這個選項會大幅提升效能，因為只在大量複製作業期間保留鎖定，會減少競爭資料表鎖定的情況。 如果資料表沒有索引，且指定了 **TABLOCK**，多個用戶端便可以同時載入這份資料表。 根據預設，鎖定行為由資料表選項 **table lock on bulk load** (大量載入時鎖定資料表) 來決定。<br /><br /> **CHECK_CONSTRAINTS**：在大量複製作業期間會檢查 *table_name* 上的任何條件約束。 依預設，會忽略條件約束。<br /><br /> **FIRE_TRIGGER**：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將資料列版本設定用於觸發程序，並將資料列版本儲存在 **tempdb** 的版本存放區內。 因此，即使啟用了觸發程序，也可以使用記錄最佳化。 在觸發程序啟用的情況下，您可能需要先擴充 **tempdb** 的大小，然後才能大量匯入具有大量資料列的批次。|  
  
### <a name="using-file-based-bulk-copy-operations"></a>使用以檔案為基礎的大量複製作業  
 OLE DB Driver for SQL Server 實作 **IBCPSession** 介面，以公開對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以檔案為基礎之大量複製作業的支援。 **IBCPSession** 介面會實作 [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)、[IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)、[IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)、[IBCPSession::BCPDone](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)[IBCPSession::BCPExec](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)、[IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)、[IBCPSession::BCPReadFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) 和 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 方法。  
  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [資料來源屬性 &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   

