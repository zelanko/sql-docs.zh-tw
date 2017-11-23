---
title: "SQL Server Native Client 功能 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
caps.latest.revision: "59"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a4bdab61611f392315c06eefa15b0830b12968b6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-native-client-features"></a>SQL Server Native Client 功能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  除了公開 Windows (先前稱為 Microsoft) Data Access Components (WDAC) 的功能之外，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 也會實作其他許多功能來公開 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能。  
  
## <a name="in-this-section"></a>本節內容  
 [ODBC 驅動程式在處理字元轉換上的行為變更](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 討論自從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client 起的行為變更。  
  
 [使用資料庫鏡像](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 討論如何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端支援使用鏡像資料庫，也就是要保留的複本或鏡像的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]待命伺服器上的資料庫。  
  
 [執行非同步作業](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援非同步作業，這是立即傳回而不在呼叫執行緒上封鎖的功能。  
  
 [使用 Multiple Active Result Set &#40;MARS&#41;](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援 Multiple Active Result Set (MARS)。 MARS 可讓您使用單一資料庫連接執行與接收多個結果集  
  
 [使用 XML 資料類型](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援 XML 資料類型，這是以 XML 為基礎的資料類型，可以當做資料行類型、變數類型、參數類型或函數傳回類型使用。  
  
 [使用使用者定義型別](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 討論如何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端支援使用者定義型別 (UDT)，這會擴充 SQL 類型系統，可讓您將物件和自訂資料結構中的儲存[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  
  
 [使用大型實值型別](../../../relational-databases/native-client/features/using-large-value-types.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援大數值資料類型，也就是大型物件資料類型 (LOB)。  
  
 [以程式設計方式變更密碼](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援過期密碼的處理方式，讓密碼現在可以在用戶端上變更，而不需要系統管理員介入。  
  
 [使用快照隔離](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援資料列版本設定的增強功能，藉由避免發生讀取器-寫入器封鎖的情況來改善效能。  
  
 [使用查詢通知](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援在資料列集修改時使用取用者通知。  
  
 [執行大量複製作業](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 討論如何[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端支援大量複製作業可讓大量的資料傳輸，進入或離開[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表或檢視表。  
  
 [使用加密而不需驗證](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 討論如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 加密傳送到伺服器的資料，而不驗證憑證。  
  
 [資料表值參數 &#40;SQL Server Native Client &#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對於資料表值參數的支援。  
  
 [大型 CLR 使用者定義型別](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 討論大型 Common Language Runtime (CLR) 使用者定義型別 (UDT) 的支援。  
  
 [FILESTREAM 支援](../../../relational-databases/native-client/features/filestream-support.md)  
 討論[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 對增強型 FILESTREAM 功能的支援。  
  
 [服務主要名稱 &#40;SPN &#41;用戶端連接中的支援](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 討論如何擴充服務主要名稱 (SPN) 的支援以便跨所有通訊協定進行相互驗證。  
  
 [SQL Server Native Client 支援疏鬆資料行](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對疏鬆資料行的支援。  
  
 [日期和時間改善](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 討論針對新日期和時間資料類型加入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的支援。  
  
 [中繼資料探索](../../../relational-databases/native-client/features/metadata-discovery.md)  
 討論在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 內所做的中繼資料探索改進。  
  
 [SQL Server Native Client 11.0 中的 UTF-16 支援](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 討論 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中導入的行為變更。 如果繫結資料行結果或輸出參數時，會提供固定長度的緩衝區，而且**wchar**字元結束的字元 surrogate 字組的高 surrogate 字碼指標之前，如果寫入緩衝區的下一步**wchar**字元是低 surrogate 字碼指標，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端不會將高 surrogate 字碼指標加入緩衝區。  
  
 [高可用性/災害復原的 SQL Server Native Client 支援](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 討論如何設定您的應用程式，以利用加入功能的高可用性、 嚴重損壞修復的[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
 [存取擴充事件記錄檔中的診斷資訊](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 討論可讓您存取信號緩衝區和 XEvents 記錄檔中之診斷資訊的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 及資料追蹤增強功能。  
  
 [SQL Server Native Client 支援 LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對 LocalDB 功能的支援。  
  
## <a name="see-also"></a>請參閱＜  
 [SQL Server Native Client 程式設計](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 使用說明主題](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 的使用說明主題](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [安裝 SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
