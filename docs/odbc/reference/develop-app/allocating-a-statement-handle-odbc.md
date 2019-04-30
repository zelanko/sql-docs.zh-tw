---
title: 配置陳述式控制代碼 ODBC |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9524f2e6b01d2a5827dcface3159b7c52a728c59
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287864"
---
# <a name="allocating-a-statement-handle-odbc"></a>配置陳述式控制代碼 ODBC
應用程式可以執行陳述式之前，必須配置陳述式控制代碼，如下所示：  
  
1.  應用程式宣告型別 HSTMT 的變數。 然後它會呼叫**SQLAllocHandle** ，並將傳遞這個變數，用來配置陳述式，並利用 SQL_HANDLE_STMT 選項連接的控制代碼位址。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驅動程式管理員會配置用來儲存和呼叫的陳述式的相關資訊的結構**SQLAllocHandle** SQL_HANDLE_STMT 選項與驅動程式中。  
  
3.  驅動程式配置自己的結構，用來儲存有關陳述式的資訊，並傳回驅動程式陳述式控制代碼給驅動程式管理員。  
  
4.  驅動程式管理員會回到應用程式變數中的應用程式中的驅動程式管理員陳述式控制代碼。  
  
 陳述式控制代碼識別呼叫 ODBC 函數時要使用哪一個陳述式。 如需有關陳述式控制代碼的詳細資訊，請參閱[陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)。
