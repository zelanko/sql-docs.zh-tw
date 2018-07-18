---
title: SQLSetScrollOptions 對應 |Microsoft 文件
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
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4339f395ae4c554a7ad8ca2e554769d8b27cdd4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911613"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 對應
當應用程式呼叫**SQLSetScrollOptions**透過 ODBC 3 *.x*驅動程式和驅動程式不支援**SQLSetScrollOptions**，呼叫  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 將會產生，如下所示：  
  
-   呼叫  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     與*資訊類型*引數設定為下表，根據的值中值的其中一個*KeysetSize*引數中的**SQLSetScrollOptions**。  
  
    |*KeysetSize 引數*|*資訊類型引數*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |值大於*RowsetSize*引數|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果值*KeysetSize*引數未列在上表中，呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1107 （資料列的值超出範圍） 的下列步驟都與執行。  
  
     驅動程式管理員，然後確認是否要將適當的位元設定在 **InfoValuePtr*呼叫所傳回的值**SQLGetInfo**，根據的值*並行*引數中的**SQLSetScrollOptions**。  
  
    |*並行*引數|*資訊類型*設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*並行*引數不是其中一個值，在上表中，呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1108 （並行選項超出範圍） 的下列步驟都與執行。 如果未設定適當的位元 （做為上表中所指示） **InfoValuePtr*的值會對應至其中一個*並行*引數，會呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1C00 （驅動程式不支援），且無下列步驟執行。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     與 *\*ValuePtr*設定為下表，根據的值中值的其中一個*KeysetSize*引數中的**SQLSetScrollOptions**。  
  
    |*KeysetSize*引數|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |值大於*RowsetSize*引數|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     與 *\*ValuePtr*設*並行*引數中的**SQLSetScrollOptions**。  
  
-   如果*KeysetSize*引數在呼叫**SQLSetScrollOptions**是正數，呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     與 *\*ValuePtr*設*KeysetSize*引數中的**SQLSetScrollOptions**。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     與 *\*ValuePtr*設*RowsetSize*引數中的**SQLSetScrollOptions**。  
  
    > [!NOTE]  
    >  當驅動程式管理員會將對應**SQLSetScrollOptions**應用程式使用 ODBC 3 *.x*不支援的驅動程式**SQLSetScrollOptions**，驅動程式管理員設定 SQL_ROWSET_SIZE 陳述式選項，而不將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性， *RowsetSize*引數中的**SQLSetScrollOption**。 如此一來， **SQLSetScrollOptions**不可由應用程式在呼叫提取多個資料列時， **SQLFetch**或**SQLFetchScroll**。 它可以用於擷取多個資料列呼叫時，只有**SQLExtendedFetch**。
