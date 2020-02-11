---
title: 配置連接控制碼 ODBC |Microsoft Docs
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
ms.openlocfilehash: 3bd3a44fe4f0466dfcf11a72fa0377564c1cf02f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077203"
---
# <a name="allocating-a-connection-handle-odbc"></a>配置連線控制代碼 ODBC
在應用程式可以連接至資料來源或驅動程式之前，它必須配置連接控制碼，如下所示：  
  
1.  應用程式會宣告 SQLHDBC 類型的變數。 然後它會呼叫**SQLAllocHandle** ，並傳遞這個變數的位址、配置連接的環境控制碼，以及 SQL_HANDLE_DBC 選項。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存語句相關資訊的結構，並傳回變數中的連接控制碼。  
  
 驅動程式管理員目前不會呼叫驅動程式中的**SQLAllocHandle** ，因為它不知道要呼叫哪一個驅動程式。 在應用程式呼叫函式以連接到資料來源之前，它會延遲在驅動程式中呼叫**SQLAllocHandle** 。 如需詳細資訊，請參閱本節稍後[的連接程式中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 請務必注意，配置連接控制碼與載入驅動程式並不相同。 在呼叫連接函式之前，不會載入驅動程式。 因此，在配置連接控制碼之後，以及連接到驅動程式或資料來源之前，應用程式可以使用此連接控制碼呼叫的唯一函數是**SQLSetConnectAttr**、 **SQLGetConnectAttr**或**SQLGetInfo** ，並具有 SQL_ODBC_VER 選項。 使用連接控制碼呼叫其他函式（例如**SQLEndTran**）會傳回 SQLSTATE 08003 （連接未開啟）。 如需完整的詳細資訊，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需連接控制碼的詳細資訊，請參閱[連接控制碼](../../../odbc/reference/develop-app/connection-handles.md)。
