---
title: 配置敘述的句柄 ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288428"
---
# <a name="allocating-a-statement-handle-odbc"></a>配置陳述式控制代碼 ODBC
在應用程式可以執行語句之前,它必須分配語句句柄,如下所示:  
  
1.  應用程式聲明 HSTMT 類型的變數。 然後,它調用**SQLAllocHandle**並傳遞此變數的位址、要在其中分配語句的連接的句柄以及SQL_HANDLE_STMT選項。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驅動程式管理員分配一個結構,用於存儲有關語句的資訊,並在驅動程式中調用**SQLAllocHandle,** 並帶有SQL_HANDLE_STMT選項。  
  
3.  驅動程式分配自己的結構,以存儲有關語句的資訊,並將驅動程式語句句柄返回到驅動程式管理器。  
  
4.  驅動程式管理員將驅動程式管理器語句句柄返回到應用程式變數中的應用程式。  
  
 語句句柄標識調用 ODBC 函數時要使用的語句。 有關語句句柄的詳細資訊,請參閱[語句句柄](../../../odbc/reference/develop-app/statement-handles.md)。
