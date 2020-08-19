---
description: SQLSetScrollOptions 對應
title: SQLSetScrollOptions 對應 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 111fb84cd584e23b18d889634893556de86311a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476920"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLSetScrollOptions**時，驅動程式不支援**SQLSetScrollOptions**，而是呼叫  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 將會產生如下的結果：  
  
-   呼叫  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     將*InfoType*引數設定為下表中的其中一個值，取決於**SQLSetScrollOptions**中的*KeysetSize*引數值。  
  
    |*KeysetSize 引數*|*InfoType 引數*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |大於 *RowsetSize* 引數的值|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果 *KeysetSize* 引數的值未列于上表中，則對 **SQLSetScrollOptions** 的呼叫會傳回 SQLSTATE S1107 (Row 值超出範圍) ，而且不會執行下列任何步驟。  
  
     然後，驅動程式管理員會根據**SQLSetScrollOptions**中*Concurrency*引數的值，驗證是否已在呼叫**SQLGetInfo**所傳回的 **InfoValuePtr*值中設定適當的位。  
  
    |*Concurrency* 引數|*InfoType* 設定|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果 *並行* 存取引數不是上表中的其中一個值，呼叫 **SQLSETSCROLLOPTIONS** 會傳回 SQLSTATE S1108 (並行選項超出範圍) ，而且不會執行下列任何步驟。 如果上表中所示的適當位 () 未在 **InfoValuePtr* 中設定為對應至 *Concurrency* 引數的其中一個值，則對 **SQLSETSCROLLOPTIONS** 的呼叫會傳回 SQLSTATE S1C00 (驅動程式無法) ，且不會執行下列任何步驟。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     根據**SQLSetScrollOptions**中*KeysetSize*引數的值，將* \* ValuePtr*設為下表中的其中一個值。  
  
    |*KeysetSize* 引數|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |大於 *RowsetSize* 引數的值|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     將* \* ValuePtr*設定為**SQLSetScrollOptions**中的*Concurrency*引數。  
  
-   如果**SQLSetScrollOptions**呼叫中的*KeysetSize*引數是正數，則呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     將* \* ValuePtr*設定為**SQLSetScrollOptions**中的*KeysetSize*引數。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     將* \* ValuePtr*設定為**SQLSetScrollOptions**中的*RowsetSize*引數。  
  
    > [!NOTE]  
    >  當驅動程式管理員針對使用不支援**SQLSetScrollOptions***之 ODBC 3.x 驅動程式的*應用程式對應**SQLSetScrollOptions**時，驅動程式管理員會將 SQL_ROWSET_SIZE 語句選項（而非 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性）設定為**SQLSetScrollOption**中的*RowsetSize*引數。 因此，應用程式在呼叫**SQLFetch**或**SQLFetchScroll**時，無法使用**SQLSetScrollOptions**來提取多個資料列。 只有在透過呼叫 **SQLExtendedFetch**來提取多個資料列時，才可以使用它。
