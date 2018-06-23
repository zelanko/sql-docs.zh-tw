---
title: 大量複製函數 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], functions
- ODBC, bulk copy operations
- functions [ODBC]
ms.assetid: 6526b892-1d58-4f55-8335-f09887f6ea02
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4a4ec7390e5548acadd872a6e43be83e7710d86b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144924"
---
# <a name="bulk-copy-functions"></a>大量複製函數
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專用大量複製 API 延伸模組可讓用戶端應用程式在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，快速加入或擷取資料列。  
  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 時，您可以參考 SQLNCLI11.LIB 和 SQLNCLI.H 中的大量複製函數 (BCP)。  
  
 使用 BCP API 函數呼叫的應用程式應該與應用程式使用之驅動程式 (.dll) 隨附的程式庫 (.lib) 連結。 BCP 應用程式不應該連結一個以上的驅動程式庫。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [bcp_batch](bcp-batch.md)  
  
-   [bcp_bind](bcp-bind.md)  
  
-   [bcp_colfmt](bcp-colfmt.md)  
  
-   [bcp_collen](bcp-collen.md)  
  
-   [bcp_colptr](bcp-colptr.md)  
  
-   [bcp_columns](bcp-columns.md)  
  
-   [bcp_control](bcp-control.md)  
  
-   [bcp_done](bcp-done.md)  
  
-   [bcp_exec](bcp-exec.md)  
  
-   [bcp_getcolfmt](bcp-getcolfmt.md)  
  
-   [bcp_gettypename](bcp-gettypename.md)  
  
-   [bcp_init](bcp-init.md)  
  
-   [bcp_moretext](bcp-moretext.md)  
  
-   [bcp_readfmt](bcp-readfmt.md)  
  
-   [bcp_sendrow](bcp-sendrow.md)  
  
-   [bcp_setbulkmode](bcp-setbulkmode.md)  
  
-   [bcp_setcolfmt](bcp-setcolfmt.md)  
  
-   [bcp_writefmt](bcp-writefmt.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 驅動程式延伸模組](../../database-engine/dev-guide/sql-server-driver-extensions.md)   
 [執行大量複製作業&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  