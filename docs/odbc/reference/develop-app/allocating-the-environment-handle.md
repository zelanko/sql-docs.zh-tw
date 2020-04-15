---
title: 配置環境句柄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303001"
---
# <a name="allocating-the-environment-handle"></a>配置環境控制代碼
任何 ODBC 應用程式的第一個任務是載入驅動程式管理員;如何做到這一點取決於操作系統。 例如,在運行 Microsoft ® Windows NT® 伺服器/Windows 2000 伺服器、Windows NT 工作站/Windows 2000 專業版或 Microsoft Windows ® 95/98 的電腦上,應用程式要麼連結到驅動程式管理器庫,要麼調用**LoadLibrary**來載入驅動程式管理器 DLL。  
  
 下一個工作,必須在應用程式呼叫任何其他 ODBC 函數之前完成,是初始化 ODBC 環境並分配環境句柄,如下所示:  
  
1.  應用程式聲明 SQLHENV 類型的變數。 然後,它調用**SQLAllocHandle**並傳遞此變數的位址和SQL_HANDLE_ENV選項。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驅動程式管理員分配一個結構,用於存儲有關環境的資訊,並在變數中返回環境句柄。  
  
 驅動程式管理器此時不會在驅動程式中調用**SQLAllocHandle,** 因為它不知道要調用哪個驅動程式。 它會延遲在驅動程式中調用**SQLAllocHandle,** 直到應用程式呼叫函數以連接到資料來源。 有關詳細資訊,請參閱[驅動程式管理器在連接過程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md),請參閱本節後面的部分。  
  
 當應用程式完成使用 ODBC 後,它將使用**SQLFreeHandle**釋放環境句柄。 釋放環境後,在調用 ODBC 函數時使用環境的句柄是一種應用程式程式設計錯誤;這樣做有未定義,但可能是致命的後果。  
  
 調用**SQLFreeHandle**時,驅動程式將釋放用於存儲有關環境的資訊的結構。 請注意,在釋放該環境句柄上的所有連接句柄之前,無法為環境句柄調用**SQLFreeHandle。**  
  
 關於環境句柄的詳細資訊,請參閱[環境句柄](../../../odbc/reference/develop-app/environment-handles.md)。
