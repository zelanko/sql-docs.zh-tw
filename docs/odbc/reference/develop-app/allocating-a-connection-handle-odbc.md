---
title: 配置連接控制代碼 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288320"
---
# <a name="allocating-a-connection-handle-odbc"></a>配置連線控制代碼 ODBC
應用程式可以連接到資料來源或驅動程式之前，必須配置連接控制代碼，如下所示：  
  
1.  應用程式宣告型別 SQLHDBC 的變數。 然後它會呼叫**SQLAllocHandle** ，並將傳遞這個變數，在其中配置的連接，並利用 SQL_HANDLE_DBC 選項環境的控制代碼位址。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存資訊的陳述式中的結構，並傳回在變數中的連接控制代碼。  
  
 驅動程式管理員不會呼叫**SQLAllocHandle**此驅動程式中的時間，因為它不知道要呼叫哪一個驅動程式。 它會延遲呼叫**SQLAllocHandle**驅動程式，直到應用程式呼叫的函式，來連接到資料來源中。 如需詳細資訊，請參閱 <<c0> [ 在連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)稍後這一節。  
  
 請務必注意，配置連接控制代碼不載入驅動程式相同。 連線函式呼叫之前，不會載入驅動程式。 因此，在配置連接控制代碼之後，並連接到資料來源的驅動程式之前，應用程式可以呼叫具有連接控制代碼的唯一功能是**SQLSetConnectAttr**， **SQLGetConnectAttr**，或**SQLGetInfo** SQL_ODBC_VER 選項。 呼叫其他函式與連接的控制代碼，例如**SQLEndTran**，會傳回 SQLSTATE 08003 （未開啟連接）。 完整的詳細資訊，請參閱[附錄 b:狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需有關連接控制代碼的詳細資訊，請參閱 <<c0> [ 連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)。
