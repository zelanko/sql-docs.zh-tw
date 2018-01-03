---
title: "配置連接控制代碼 ODBC |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd1f07d35356efda77edeaf08d851ad4d7d9bcb0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="allocating-a-connection-handle-odbc"></a>配置連接控制代碼 ODBC
應用程式可以連接到資料來源或驅動程式之前，必須配置連接控制代碼，如下所示：  
  
1.  應用程式宣告 SQLHDBC 類型的變數。 然後它會呼叫**SQLAllocHandle**並將這個變數，在其中配置連接，並利用 SQL_HANDLE_DBC 選項環境的控制代碼位址。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存資訊有關陳述式中的結構，並傳回連接控制代碼變數中。  
  
 驅動程式管理員不會呼叫**SQLAllocHandle**此驅動程式中的時間，因為它不知道要呼叫哪一個驅動程式。 它會延遲呼叫**SQLAllocHandle**驅動程式，直到應用程式呼叫的函式，來連接到資料來源中。 如需詳細資訊，請參閱[連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)稍後這一節。  
  
 請務必注意，配置連接控制代碼不載入驅動程式相同。 驅動程式未載入連接函式呼叫之前。 因此之後配置連接控制代碼,，並連線到驅動程式或資料來源之前，應用程式可以呼叫具有連接控制代碼的唯一功能是**SQLSetConnectAttr**， **SQLGetConnectAttr**，或**SQLGetInfo** SQL_ODBC_VER 選項。 呼叫其他函式與連接控制代碼，例如**SQLEndTran**，會傳回 SQLSTATE 08003 （未開啟連接）。 完整的詳細資訊，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需連接控制代碼的詳細資訊，請參閱[連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)。
