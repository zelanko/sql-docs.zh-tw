---
title: 配置陳述式控制代碼 ODBC |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0f2bd2da071bb690443df9d5c0bdebb5a5e1e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908903"
---
# <a name="allocating-a-statement-handle-odbc"></a>配置陳述式控制代碼 ODBC
應用程式可以執行陳述式之前，必須配置陳述式控制代碼，如下所示：  
  
1.  應用程式宣告 HSTMT 類型的變數。 然後它會呼叫**SQLAllocHandle**並將這個變數的位址，來配置陳述式，並利用 SQL_HANDLE_STMT 選項中的連接控制代碼。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存的陳述式和呼叫資訊的結構**SQLAllocHandle** SQL_HANDLE_STMT 選項與驅動程式中。  
  
3.  驅動程式配置自己用來儲存資訊有關陳述式的結構，並傳回驅動程式陳述式控制代碼給驅動程式管理員。  
  
4.  驅動程式管理員驅動程式管理員陳述式控制代碼傳回應用程式變數中的應用程式。  
  
 陳述式控制代碼識別哪些陳述式來呼叫 ODBC 函數時使用。 如需陳述式控制代碼的詳細資訊，請參閱[陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)。
