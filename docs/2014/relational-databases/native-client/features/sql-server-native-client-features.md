---
title: SQL Server Native Client 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: rothja
ms.author: jroth
ms.openlocfilehash: cc6fbe3ceb6a00df40ab7a1ac777ffaefa87cfe8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017311"
---
# <a name="sql-server-native-client-features"></a>SQL Server Native Client 功能
  除了公開 Windows (先前稱為 Microsoft) Data Access Components (WDAC) 的功能之外，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 也會實作其他許多功能來公開 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能。  
  
## <a name="in-this-section"></a>本節內容  
 [ODBC 驅動程式在處理字元轉換上的行為變更](odbc-driver-behavior-change-when-handling-character-conversions.md)  
 討論自從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client 起的行為變更。  
  
 [使用資料庫鏡像](using-database-mirroring.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援鏡像資料庫的使用，這是在待命伺服器上保留資料庫複本或鏡像的功能 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 [執行非同步作業](performing-asynchronous-operations.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援非同步作業，這是立即傳回而不在呼叫執行緒上封鎖的功能。  
  
 [使用 Multiple Active Result Set &#40;MARS&#41;](using-multiple-active-result-sets-mars.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援 Multiple Active Result Set (MARS)。 MARS 可讓您使用單一資料庫連接執行與接收多個結果集  
  
 [使用 XML 資料類型](using-xml-data-types.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援 XML 資料類型，這是以 XML 為基礎的資料類型，可以當做資料行類型、變數類型、參數類型或函數傳回類型使用。  
  
 [使用使用者定義型別](using-user-defined-types.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援使用者定義型別（UDT），它可讓您將物件和自訂資料結構儲存在資料庫中，藉此擴充 SQL 類型系統 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 [使用大數值類型](using-large-value-types.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援大數值資料類型，也就是大型物件資料類型 (LOB)。  
  
 [以程式設計方式變更密碼](changing-passwords-programmatically.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援過期密碼的處理方式，讓密碼現在可以在用戶端上變更，而不需要系統管理員介入。  
  
 [使用快照隔離](working-with-snapshot-isolation.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援資料列版本設定的增強功能，藉由避免發生讀取器-寫入器封鎖的情況來改善效能。  
  
 [使用查詢通知](working-with-query-notifications.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援在資料列集修改時使用取用者通知。  
  
 [執行大量複製作業](performing-bulk-copy-operations.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 如何支援大量複製作業，以允許在資料表或視圖中傳入或傳出大量資料 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 [使用加密而不需驗證](using-encryption-without-validation.md)  
 討論如何使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 加密傳送到伺服器的資料，而不驗證憑證。  
  
 [資料表值參數 &#40;SQL Server Native Client&#41;](table-valued-parameters-sql-server-native-client.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對於資料表值參數的支援。  
  
 [大型 CLR 使用者定義型別](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 討論大型 Common Language Runtime (CLR) 使用者定義型別 (UDT) 的支援。  
  
 [FILESTREAM 支援](filestream-support.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對增強型 FILESTREAM 功能的支援。  
  
 [用戶端連接中的服務主要名稱 &#40;SPN&#41; 支援](service-principal-name-spn-support-in-client-connections.md)  
 討論如何擴充服務主要名稱 (SPN) 的支援以便跨所有通訊協定進行相互驗證。  
  
 [SQL Server Native Client 中的疏鬆資料行支援](sparse-columns-support-in-sql-server-native-client.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對疏鬆資料行的支援。  
  
 [日期和時間改善](date-and-time-improvements.md)  
 討論針對新日期和時間資料類型加入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的支援。  
  
 [中繼資料探索](metadata-discovery.md)  
 討論在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 內所做的中繼資料探索改進。  
  
 [SQL Server Native Client 11.0 中的 UTF-16 支援](utf-16-support-in-sql-server-native-client-11-0.md)  
 討論 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中導入的行為變更。 如果您在繫結資料行結果或輸出參數時提供固定長度的緩衝區、`wchar` 字元在終止字元成為 Surrogate 字組的高 Surrogate 字碼指標之前寫入緩衝區，而且下一個 `wchar` 字元是低 Surrogate 字碼指標，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 就不會將高 Surrogate 字碼指標加入至緩衝區。  
  
 [高可用性/災害復原的 SQL Server Native Client 支援](sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 討論如何設定應用程式以利用 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中新增的高可用性災害復原功能。  
  
 [存取擴充事件記錄檔中的診斷資訊](accessing-diagnostic-information-in-the-extended-events-log.md)  
 討論可讓您存取信號緩衝區和 XEvents 記錄檔中之診斷資訊的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 及資料追蹤增強功能。  
  
 [SQL Server Native Client 對 LocalDB 的支援](sql-server-native-client-support-for-localdb.md)  
 討論 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 對 LocalDB 功能的支援。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../sql-server-native-client-programming.md)   
 [ODBC 的使用說明主題](../../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB how to 主題](../../native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [安裝 SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
