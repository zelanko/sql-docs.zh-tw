---
title: 配置連接句柄 ODBC |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288518"
---
# <a name="allocating-a-connection-handle-odbc"></a>配置連線控制代碼 ODBC
在應用程式可以連接到資料來源或驅動程式之前,它必須分配連接句柄,如下所示:  
  
1.  應用程式聲明 SQLHDBC 類型的變數。 然後,它調用**SQLAllocHandle**並傳遞此變數的位址、要分配連接的環境的句柄以及SQL_HANDLE_DBC選項。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驅動程式管理員分配一個結構,用於存儲有關語句的資訊並在變數中返回連接句柄。  
  
 驅動程式管理器此時不會在驅動程式中調用**SQLAllocHandle,** 因為它不知道要調用哪個驅動程式。 它會延遲在驅動程式中調用**SQLAllocHandle,** 直到應用程式呼叫函數以連接到資料來源。 有關詳細資訊,請參閱[驅動程式管理器在連接過程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md),請參閱本節後面的部分。  
  
 請務必注意,分配連接句柄與載入驅動程式不同。 在調用連接函數之前,不會載入驅動程式。 因此,在分配連接句柄後,在連接到驅動程式或數據源之前,應用程式可以使用連接句柄調用的唯一函數是**SQLSetConnectAttr、SQLGetConnectAttr**或**SQLGetInfo,** 帶**SQLGetConnectAttr**有SQL_ODBC_VER選項。 使用連接句柄調用其他函數(如**SQLEndTran**)傳回 SQLSTATE 08003(連接未打開)。 關於完整詳細資訊,請參閱[入 B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有關連接句柄的詳細資訊,請參閱[連接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
