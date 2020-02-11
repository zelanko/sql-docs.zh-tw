---
title: 中繼資料探索 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 380d76fe0740a6c43584a68f9353d85539867fe3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761405"
---
# <a name="metadata-discovery"></a>中繼資料探索
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  中[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的中繼資料探索改進[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可讓原生用戶端應用程式確保查詢執行所傳回的資料行或參數中繼資料，與您在執行查詢之前指定的元資料格式完全相同或相容。 如果查詢執行之後傳回的中繼資料與您在查詢執行之前指定的中繼資料格式不相容，您就會收到錯誤。  
  
 在 bcp 和 ODBC 函數以及 IBCPSession 和 IBCPSession2 介面中，您現在可以指定延遲讀取 (延遲中繼資料探索)，避免針對查詢輸出作業進行中繼資料探索。 這樣做可改善效能並排除中繼資料探索失敗。  
  
 如果您使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的 Native Client 開發應用程式，但連接到早于[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的伺服器版本，則中繼資料探索功能將對應至伺服器的版本。  
  
## <a name="remarks"></a>備註  
 
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 bcp 函數，以便提供改良的中繼資料探索：  
  
-   [bcp_columns](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 使用[bcp_setbulkmode](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)指定元資料格式時，您也會看到效能改進。  
  
 [bcp_control](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)有一個新的*eOption* ，可控制 Bcp_readfmt 的行為： **BCPDELAYREADFMT**。  
  
 
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 ODBC 函數，以便提供改良的中繼資料探索：  
  
-   [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../../relational-databases/native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md)  
  
 
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 已經強化了下列 OLE DB 成員函數，以便提供改良的中繼資料探索：  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters：： GetParameterInfo （如需詳細資訊，請參閱[ICommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md) ）  
  
 當您使用 IBCPSession::BCPSetBulkMode 來指定中繼資料格式時，也會看見效能改進  
  
 由於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加入了下列兩個預存程序，所以您可以在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 中進行改善的中繼資料探索：  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
