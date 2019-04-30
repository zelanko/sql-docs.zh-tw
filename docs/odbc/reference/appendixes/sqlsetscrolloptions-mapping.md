---
title: SQLSetScrollOptions Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520554b509b0c25d62e4a191e16ad3524a02652
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297455"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 對應
當應用程式呼叫**SQLSetScrollOptions**透過 ODBC 3 *.x*驅動程式和驅動程式不支援**SQLSetScrollOptions**，呼叫  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 會產生，如下所示：  
  
-   呼叫  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     具有*資訊類型*引數設定為下表，根據的值中值的其中一個*KeysetSize*中的引數**SQLSetScrollOptions**。  
  
    |*KeysetSize 引數*|*資訊類型引數*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |值大於*RowsetSize*引數|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果值*KeysetSize*引數未列在上表中，呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1107 （資料列超出範圍的值） 並沒有任何下列的步驟執行。  
  
     驅動程式管理員，然後確認是否設定適當的位元 **InfoValuePtr*呼叫所傳回的值**SQLGetInfo**，根據值*並行*中的引數**SQLSetScrollOptions**。  
  
    |*並行*引數|*資訊類型*設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*並行*引數不是其中一個值，在上表中，呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1108 （超出範圍的並行選項） 並沒有任何下列的步驟執行。 如果未設定適當的位元 （做為上表中所述） **InfoValuePtr*的值會對應至其中一個*並行*引數，會呼叫**SQLSetScrollOptions**傳回 SQLSTATE S1C00 （驅動程式不支援），並且會執行下列步驟。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     具有 *\*ValuePtr*設為其中一個下表中，根據的值中的值*KeysetSize*中的引數**SQLSetScrollOptions**。  
  
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
  
     具有 *\*ValuePtr*設定為*並行*中的引數**SQLSetScrollOptions**。  
  
-   如果*KeysetSize*呼叫中的引數**SQLSetScrollOptions**是正數，呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     具有 *\*ValuePtr*設定為*KeysetSize*中的引數**SQLSetScrollOptions**。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     具有 *\*ValuePtr*設定為*RowsetSize*中的引數**SQLSetScrollOptions**。  
  
    > [!NOTE]  
    >  當驅動程式管理員會將對應**SQLSetScrollOptions**應用程式使用 ODBC 3 *.x*不支援的驅動程式**SQLSetScrollOptions**，驅動程式管理員設定 SQL_ROWSET_SIZE 陳述式選項，而不是 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性， *RowsetSize*中的引數**SQLSetScrollOption**。 如此一來， **SQLSetScrollOptions**呼叫擷取多個資料列時無法由應用程式**SQLFetch**或是**SQLFetchScroll**。 它可以用於擷取多個資料列呼叫時，才**SQLExtendedFetch**。
