---
title: "中繼資料探索 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d847a3f0a6a577b82de4bf060cdb3fdb44a71f5a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="metadata-discovery"></a>中繼資料探索
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  中的中繼資料探索改進[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]允許[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前指定原生用戶端應用程式，以確保執行查詢所傳回的資料行或參數中繼資料與相同或相容的中繼資料格式您在執行查詢。 如果查詢執行之後傳回的中繼資料與您在查詢執行之前指定的中繼資料格式不相容，您就會收到錯誤。  
  
 在 bcp 和 ODBC 函數以及 IBCPSession 和 IBCPSession2 介面中，您現在可以指定延遲讀取 (延遲中繼資料探索)，避免針對查詢輸出作業進行中繼資料探索。 這樣做可改善效能並排除中繼資料探索失敗。  
  
 如果您開發應用程式使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的原生用戶端[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]但連接到伺服器版本早於[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]，中繼資料探索功能將會對應到伺服器的版本。  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 bcp 函數，以便提供改良的中繼資料探索：  
  
-   [bcp_columns](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 您也會看見效能改進，指定中繼資料格式使用時[bcp_setbulkmode](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)。  
  
 [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)有新的*eOption*控制 bcp_readfmt 行為： **BCPDELAYREADFMT**。  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 ODBC 函數，以便提供改良的中繼資料探索：  
  
-   [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../../relational-databases/native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 OLE DB 成員函數，以便提供改良的中繼資料探索：  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   Icommandwithparameters:: Getparameterinfo (請參閱[ICommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)如需詳細資訊)  
  
 您也會指定使用 IBCPSession::BCPSetBulkMode 的中繼資料格式時看到效能改進  
  
 由於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加入了下列兩個預存程序，所以您可以在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 中進行改善的中繼資料探索：  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
