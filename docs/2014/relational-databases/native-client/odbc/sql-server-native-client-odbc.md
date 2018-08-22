---
title: SQL Server Native Client (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ae0ba38664295ed32dbf425527ccdf7a48d1313
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392535"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC 是應用程式開發介面 (API) 的標準定義，用於存取關聯式資料庫或索引循序存取方法 (ISAM) 資料庫中的資料。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援 ODBC 做為其中一個原生應用程式開發介面，來撰寫與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行通訊的 C 和 C++ 應用程式。  
  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式撰寫的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 程式會透過 C 函數呼叫，與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行通訊。 ODBC 函數的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專屬版本會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式中實作。 此驅動程式會將 SQL 陳述式傳遞到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，然後將陳述式的結果傳回到應用程式。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式符合 Microsoft Win32 ODBC 3.51 規格。 此驅動程式支援使用舊版 ODBC，以 ODBC 3.51 規格中定義之方式撰寫的應用程式。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源名稱和 64 位元作業系統](data-source-names-and-64-bit-operating-systems.md)  
  
-   [建立 SQL Server Native Client ODBC 驅動程式應用程式](creating-a-driver-application.md)  
  
-   [與 SQL Server 通訊&#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [執行查詢&#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [處理結果&#40;ODBC&#41;](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [使用資料指標&#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [執行交易&#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [處理錯誤與訊息](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [執行預存程序](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [使用目錄函式](using-catalog-functions.md)  
  
-   [執行大量複製作業&#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [管理 Text 和 Image 資料行](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [分析 ODBC 驅動程式效能](profiling-odbc-driver-performance.md)  
  
-   [資料表值參數&#40;ODBC&#41;](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [日期和時間改善&#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [大型 CLR 使用者定義型別&#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM 支援&#40;ODBC&#41;](filestream-support-odbc.md)  
  
-   [服務主體名稱&#40;Spn&#41;用戶端連接中&#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [疏鬆資料行支援&#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41;參考](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [ODBC 的使用說明主題](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../sql-server-native-client-programming.md)   
 [安裝 SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
