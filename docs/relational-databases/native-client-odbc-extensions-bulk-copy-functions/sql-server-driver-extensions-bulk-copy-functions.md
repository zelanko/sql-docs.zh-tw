---
title: "大量複製函數 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 488c3f5ec2cc7785333f80ae4bb73dc3961990a6
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sql-server-driver-extensions---bulk-copy-functions"></a>SQL Server 驅動程式延伸模組-大量複製函數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  開放式資料庫連接 (Open Database Connectivity，ODBC) 是應用程式用來在 ODBC 資料來源中存取資料的 Microsoft Win32 應用程式開發介面。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式參考不會列出所有 ODBC 函數呼叫。 只會討論與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式搭配使用時，具有驅動程式特有參數或行為的函數。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式符合 ODBC 3.51 規格。 如需 ODBC 3.51 的完整參考，下載 Microsoft Data Access Components SDK，從[資料存取和存放開發人員中心](http://go.microsoft.com/fwlink?linkid=4173)，或檢視[ODBC 程式設計人員參考](http://go.microsoft.com/fwlink/?LinkId=45250)線上。  
 
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專用大量複製 API 延伸模組可讓用戶端應用程式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，快速加入或擷取資料列。  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 時，您可以參考 SQLNCLI11.LIB 和 SQLNCLI.H 中的大量複製函數 (BCP)。  
  
 使用 BCP API 函數呼叫的應用程式應該與應用程式使用之驅動程式 (.dll) 隨附的程式庫 (.lib) 連結。 BCP 應用程式不應該連結一個以上的驅動程式庫。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)  
  
-   [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)  
  
-   [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)  
  
-   [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)  
  
-   [bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md)  
  
-   [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)  
  
-   [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)  
  
-   [bcp_getcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_gettypename](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-gettypename.md)  
  
-   [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)  
  
-   [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)  
  
-   [bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)  
  
-   [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
-   [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 驅動程式延伸模組](http://msdn.microsoft.com/library/1043bc93-965d-4939-bd1c-21e9d8d3e9ac)   
 [執行大量複製作業 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
