---
title: 執行大量複製作業 |Microsoft 文件
description: 執行使用適用於 SQL Server 的 OLE DB 驅動程式的大量複製作業
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], bulk copy operations
- OLE DB Driver for SQL Server, bulk copy operations
- MSOLEDBSQL, bulk copy operations
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fdfb6066692c2d15aa44fa8671cb590f8b009c2b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="performing-bulk-copy-operations"></a>執行大量複製作業
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製功能支援將大量資料傳送進出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表或檢視。 資料也可以藉由指定 SELECT 陳述式而向外傳送。 您可在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和作業系統資料檔 (例如 ASCII 檔) 之間移動。 資料檔可能具有不同的格式；您可將格式定義為以格式檔來大量複製。 或者，也可以使用大量複製函數和方法，將資料載入程式變數，然後傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 範例應用程式，示範這項功能，請參閱[大量資料使用 IRowsetFastLoad 大量複製&#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)。  
  
 應用程式通常會以下列其中一種方式使用大量複製：  
  
-   從資料表、檢視或 Transact-SQL 陳述式的結果集大量複製到資料檔，其中資料會以與資料表或檢視相同的格式儲存。  
  
     這稱為原生模式的資料檔案。  
  
-   從資料表、檢視或 Transact-SQL 陳述式的結果集大量複製到資料檔，其中儲存資料的格式會與資料表或檢視不同。  
  
     在此情況下，會在每一個資料行儲存到資料檔中時，為其建立另一個定義特性 (資料類型、位置、長度、結束字元等) 的格式檔案。 如果所有的資料行都轉換成字元格式，則產生的檔案稱為字元模式資料檔。  
  
-   從資料檔大量複製到資料表或檢視。  
  
     如有需要，可使用格式檔來判斷資料檔的配置。  
  
-   將資料載入程式變數，然後使用可在資料行中一次複製大量資料的大量複製函數，將資料匯入資料表或檢視。  
  
 大量複製函數所使用的資料檔不必由其他的大量複製程式建立。 任何其他的系統都可以根據大量複製定義產生資料檔和格式檔；之後可以將這些檔案搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製程式使用，以將資料匯入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 例如，您可以從試算表將資料匯出至 Tab 鍵分隔檔案、建立描述 Tab 鍵分隔檔案的格式檔，然後使用大量複製程式將資料快速匯入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 大量複製所產生的資料檔也可以匯入至其他應用程式。 例如，您可以使用大量複製函數，將資料從資料表或檢視匯出至 Tab 鍵分隔檔案，然後再將該檔案載入至試算表。  
  
 程式設計人員在撰寫使用大量複製函數的應用程式時，應該遵照大量複製良好效能的一般規則。 如需有關進行中的大量複製作業支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱[大量匯入和匯出的資料&#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 CLR 使用者定義型別 (UDT) 必須繫結為二進位資料。 即使格式檔指定 SQLCHAR 做為目標 UDT 資料行的資料類型，BCP 公用程式也會將該資料視為二進位。  
  
 請勿將 SET FMTONLY OFF 用於大量複製作業。 SET FMTONLY OFF 可能會導致大量複製作業失敗或提供未預期的結果。  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式 
 SQL Server OLE DB 驅動程式會實作兩種方法來執行大量複製作業與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。 第一種方法牽涉到使用[IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)記憶體為基礎之大量複製作業; 和第二個介面牽涉到使用[IBCPSession](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)介面進行以檔案為基礎的大量複製作業。  
  
### <a name="using-memory-based-bulk-copy-operations"></a>使用以記憶體為基礎的大量複製作業  
 SQL Server OLE DB 驅動程式會實作**IRowsetFastLoad**介面，以公開支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]記憶體為基礎之大量複製作業。 **IRowsetFastLoad**介面會實作[irowsetfastload:: Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)和[irowsetfastload:: Insertrow](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)方法。  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>針對 IRowsetFastLoad 啟用工作階段  
 取用者，OLE DB 驅動程式的 SQL Server 特定資料來源屬性 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE，適用於 SQL Server 的大量複製其需要通知 OLE DB 驅動程式。 資料來源上設定屬性，取用者會針對 SQL Server 工作階段建立 OLE DB 驅動程式。 新的工作階段可讓取用者存取**IRowsetFastLoad**介面。  
  
> [!NOTE]  
>  如果**IDataInitialize**介面用來初始化資料來源，則必須在中設定 SSPROP_IRowsetFastLoad 屬性*rgPropertySets*參數**Iopenrowset:: Openrowset**方法; 否則呼叫**OpenRowset**方法會傳回 E_NOINTERFACE。  
  
 啟用大量複製工作階段限制的工作階段上的 SQL Server 支援的介面，OLE DB 驅動程式。 啟用大量複製功能的工作階段只會公開下列介面：  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 若要停用大量啟用複製的資料列集的建立，並會讓 OLE DB 驅動程式的 SQL Server 工作階段還原為標準處理，SSPROP_ENABLEFASTLOAD 重設為 VARIANT_FALSE。  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad Rowsets  
 SQL Server 大量複製資料列集，OLE DB 驅動程式是唯寫的但會公開允許取用者判斷結構的介面[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。 下列的介面會公開在大量複製啟用 OLE DB 驅動程式的 SQL Server 資料列集：  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 提供者特有的屬性 SSPROP_FASTLOADOPTIONS、 SSPROP_FASTLOADKEEPNULLS 和 ssprop_fastloadkeepidentity 可控制 SQL Server 大量複製資料列集的 OLE DB 驅動程式的行為。 屬性中指定*Rgpropertysets*隸屬*rgPropertySets* **IOpenRowset**參數成員。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：維護取用者所提供的識別值。<br /><br /> VARIANT_FALSE：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中識別資料行的值是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 產生。 OLE DB 驅動程式會忽略任何繫結資料行的值，適用於 SQL Server。<br /><br /> VARIANT_TRUE：取用者會繫結為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別資料行提供值的存取子。 識別屬性不是可接受 null 值，讓取用者提供有關每個唯一值的資料行上**irowsetfastload:: Insert**呼叫。|  
|SSPROP_FASTLOADKEEPNULLS|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：針對具有 DEFAULT 條件約束的資料行維護 NULL。 只對接受 NULL 且套用 DEFAULT 條件約束的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行造成影響。<br /><br /> VARIANT_FALSE:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時，OLE DB 驅動程式的 SQL Server 取用者插入的資料行包含 NULL 的資料列插入資料行的預設值。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server 取用者，OLE DB 驅動程式插入資料行包含 NULL 的資料列時，插入 NULL 資料行值。|  
|SSPROP_FASTLOADOPTIONS|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BSTR<br /><br /> 預設值：無<br /><br /> 描述： 這個屬性等同於 **-h** "*提示*[，...*n*]"選項**bcp**公用程式。 將資料大量複製到資料表時，可使用下列字串做為選項。<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,...*n*]): 資料檔中資料的排序順序。 如果載入的資料檔是依照資料表的叢集索引來排序，將可增進大量複製的效能。<br /><br /> **ROWS_PER_BATCH** = *bb*： 每一批資料的資料列數目 (作為*bb*)。 伺服器根據 *bb*值，將大量載入最佳化。 根據預設， **ROWS_PER_BATCH**不明。<br /><br /> **KILOBYTES_PER_BATCH** = *cc*： 數量 (kb) 的每個批次 （如 cc) 的資料。 根據預設， **KILOBYTES_PER_BATCH**不明。<br /><br /> **TABLOCK**： 大量複製作業期間取得資料表層級鎖定。 這個選項會大幅提升效能，因為只在大量複製作業期間保留鎖定，會減少競爭資料表鎖定的情況。 可以同時載入這份多個用戶端如果資料表沒有索引和**TABLOCK**指定。 根據預設，鎖定行為由資料表選項**資料表鎖定大量載入**。<br /><br /> **CHECK_CONSTRAINTS**： 任何條件約束*table_name*大量複製作業期間，會檢查。 依預設，會忽略條件約束。<br /><br /> **FIRE_TRIGGER**:[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]用於觸發程序中的資料列版本設定和版本存放區中儲存的資料列版本**tempdb**。 因此，即使啟用了觸發程序，也可以使用記錄最佳化。 大量匯入具有大量的資料列的批次啟用觸發程序前,，您可能需要擴充的大小**tempdb**。|  
  
### <a name="using-file-based-bulk-copy-operations"></a>使用以檔案為基礎的大量複製作業  
 SQL Server OLE DB 驅動程式會實作**IBCPSession**介面，以公開支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]以檔案為基礎的大量複製作業。 **IBCPSession**介面會實作[ibcpsession:: Bcpcolfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)， [ibcpsession:: Bcpcolumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)， [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)， [IBCPSession::BCPDone](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)， [Bcpexec](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)， [ibcpsession:: Bcpinit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)， [ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)，和[ibcpsession:: Bcpwritefmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)方法。  
  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 功能的 OLE DB 驅動程式](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [資料來源屬性&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [最佳化大量匯入效能](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  

