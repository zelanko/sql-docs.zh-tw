---
title: SQL Server 功能的 OLE DB 驅動程式 |Microsoft 文件
description: OLE DB 驅動程式的 SQL Server 功能
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3f1cc26981dae02bd76133c204c5eff142db76c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-driver-for-sql-server-features"></a>SQL Server 功能的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  除了公開 Windows (先前稱為 Microsoft) Data Access Components (WDAC) 功能，OLE DB 驅動程式的 SQL Server 也會實作其他許多功能來公開[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能。  
  
## <a name="in-this-section"></a>本節內容    
 [使用資料庫鏡像](../../oledb/features/using-database-mirroring.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援使用鏡像資料庫，也就是要保留的複本或鏡像的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]待命伺服器上的資料庫。  
  
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)  
 討論 OLE DB 驅動程式如何適用於 SQL Server 支援非同步作業，這是立即傳回而不會封鎖呼叫執行緒上的功能。  
  
 [使用 Multiple Active Result Set &#40;MARS&#41;](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援 multiple active result set (MARS)。 MARS 可讓您使用單一資料庫連接執行與接收多個結果集  
  
 [使用 XML 資料類型](../../oledb/features/using-xml-data-types.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援 XML 資料類型，這是可用來當做資料行類型、 變數型別、 參數類型或函式傳回類型的 XML 資料類型。  
  
 [使用使用者定義型別](../../oledb/features/using-user-defined-types.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援使用者定義型別 (UDT)，這會擴充 SQL 類型系統，可讓您將物件和自訂資料結構中的儲存[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  
  
 [使用大型值型別](../../oledb/features/using-large-value-types.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援大數值資料類型，也就是大型物件資料類型 (LOB)。  
  
 [以程式設計方式變更密碼](../../oledb/features/changing-passwords-programmatically.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援過期密碼的處理，以便現在會在沒有系統管理員介入的用戶端上變更密碼。  
  
 [使用快照隔離](../../oledb/features/working-with-snapshot-isolation.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援藉由避免發生讀取器-寫入器封鎖的情況，可改進資料庫效能的資料列版本設定的增強功能。  
  
 [使用查詢通知](../../oledb/features/working-with-query-notifications.md)  
 討論如何 OLE DB 驅動程式的 SQL Server 支援在資料列集修改的取用者通知。  
  
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)  
 討論 OLE DB 驅動程式的 SQL Server 如何支援大量複製作業可讓大量的資料傳輸，進入或離開[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表或檢視表。  
  
 [使用加密而不需驗證](../../oledb/features/using-encryption-without-validation.md)  
 討論如何使用 OLE DB 驅動程式的 SQL Server 加密資料傳送到伺服器，而不驗證憑證。  
  
 [資料表值參數&#40;for SQL Server 的 OLE DB 驅動程式&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 如需 SQL Server 支援資料表值參數的討論 OLE DB 驅動程式。  
  
 [大型 CLR 使用者定義型別](../../oledb/features/large-clr-user-defined-types.md)  
 討論大型 Common Language Runtime (CLR) 使用者定義型別 (UDT) 的支援。  
  
 [FILESTREAM 支援](../../oledb/features/filestream-support.md)  
 討論對增強型 FILESTREAM 功能的 SQL Server 支援的 OLE DB 驅動程式。  
  
 [服務主體名稱&#40;SPN&#41;中用戶端連線的支援](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 討論如何擴充服務主要名稱 (SPN) 的支援以便跨所有通訊協定進行相互驗證。  
  
 [OLE DB Driver for SQL Server 中支援疏鬆資料行](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 如需 SQL Server 支援疏鬆資料行的討論 OLE DB 驅動程式。  
  
 [日期和時間改善](../../oledb/features/date-and-time-improvements.md)  
 討論日期和時間資料型別加入至 OLE DB 驅動程式的 SQL Server 的支援。  
  
 [中繼資料探索](../../oledb/features/metadata-discovery.md)  
 討論在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 內所做的中繼資料探索改進。  
  
 [OLE DB Driver for SQL Server 中支援 UTF-16](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 討論 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中導入的行為變更。 如果繫結資料行結果或輸出參數時，會提供固定長度的緩衝區，而且**wchar**字元結束的字元 surrogate 字組的高 surrogate 字碼指標之前，如果寫入緩衝區的下一步**wchar**字元是低 surrogate 字碼指標、 OLE DB 驅動程式的 SQL Server 不會將高 surrogate 字碼指標加入至緩衝區。  
  
 [OLE DB Driver for SQL Server 支援高可用性、災害復原](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 討論如何設定您的應用程式，以利用加入功能的高可用性、 嚴重損壞修復的[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
 [存取擴充事件記錄檔中的診斷資訊](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 討論 OLE DB 驅動程式的 SQL Server 並可讓您存取信號緩衝區和 XEvents 記錄檔中的診斷資訊的資料追蹤增強功能。  
  
 [OLE DB Driver for SQL Server 支援 LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 討論對 LocalDB 功能的 SQL Server 支援的 OLE DB 驅動程式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 OLE DB 驅動程式](../../oledb/oledb-driver-for-sql-server.md)      
 [OLE DB 的使用說明主題](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [安裝 OLE DB Driver for SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
