---
title: "配置環境控制代碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c0bbe08b13b45b47fecda5143ca419c31dfe82d5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="allocating-the-environment-handle"></a>配置環境控制代碼
任何 ODBC 應用程式的第一個工作是載入驅動程式管理員。方式與作業系統相關。 比方說，在電腦上執行 Microsoft® Windows NT® Server/Windows 2000 Server、 Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98，應用程式可能是連結到驅動程式管理員文件庫或呼叫**LoadLibrary**載入驅動程式管理員的 DLL。  
  
 下一步的工作中，應用程式可以呼叫任何 ODBC 函數必須先完成，是初始化 ODBC 環境並配置環境控制代碼，如下所示：  
  
1.  應用程式宣告 SQLHENV 類型的變數。 然後它會呼叫**SQLAllocHandle**並傳遞此變數和 SQL_HANDLE_ENV 選項的位址。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存環境的相關資訊的結構，並傳回在變數中的環境控制代碼。  
  
 驅動程式管理員不會呼叫**SQLAllocHandle**此驅動程式中的時間，因為它不知道要呼叫哪一個驅動程式。 它會延遲呼叫**SQLAllocHandle**驅動程式，直到應用程式呼叫的函式，來連接到資料來源中。 如需詳細資訊，請參閱[連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)稍後這一節。  
  
 當應用程式完成使用 ODBC 時，它會釋出環境控制代碼與**SQLFreeHandle**。 釋放後環境，它是應用程式的程式設計錯誤; ODBC 函數呼叫中使用的環境控制代碼這樣做，因此必須未定義，但可能是嚴重的後果。  
  
 當**SQLFreeHandle**呼叫時，結構用來儲存環境的相關資訊的驅動程式版本。 請注意， **SQLFreeHandle**後該環境控制代碼上的所有連接控制代碼已釋放都後，無法呼叫直到環境控制代碼。  
  
 如需環境控制代碼的詳細資訊，請參閱[環境處理](../../../odbc/reference/develop-app/environment-handles.md)。
