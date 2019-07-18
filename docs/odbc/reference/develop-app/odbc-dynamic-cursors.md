---
title: ODBC 動態資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 628de07f90de47efb0546dff84c03f56efb0674c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086305"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動態資料指標
動態資料指標只是： 動態。 它可以偵測到的成員資格、 順序和值之結果集資料指標開啟後所做的變更。 例如，假設動態資料指標擷取兩個資料列，而其他應用程式接著更新其中一個資料列並刪除另一個資料列。 如果動態資料指標則會嘗試重新提取這些資料列，它不會尋找已刪除的資料列，但會傳回更新的資料列的新值。  
  
 動態資料指標偵測所有的更新、 刪除和插入，這兩其自己和其他人所做的。 （這是交易的受到隔離層級，所設定的 SQL_ATTR_TXN_ISOLATION 連接屬性）。Sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列會反映這些變更，而且可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO、 SQL_ROW_ERROR、 SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 因為動態資料指標不會傳回已刪除的資料列外資料列集，因此無法再辨識結果集中刪除的資料列或資料列狀態陣列中對應的項目存在，它不能傳回 SQL_ROW_DELETED。 藉由呼叫更新資料列時，才傳回 SQL_ROW_ADDED **SQLSetPos**，不會在它由另一個資料指標更新。  
  
 在資料庫中實作動態資料指標的其中一種是藉由建立選擇性索引定義的成員資格，並排序結果的設定。 當其他人進行變更時，會更新索引，因為這類索引為基礎的資料指標是所有的變更影響。 可以沿著索引處理其他選取項目，此索引定義的結果集內。  
  
 藉由要求的結果集來排序的唯一索引鍵，就可以模擬動態資料指標。 這類限制，用提取，會藉由執行**選取**陳述式資料指標提取資料列的每一次。 例如，假設此陳述式所定義的結果集：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要擷取此結果集中的下一個資料列集，模擬資料指標，請設定下列的參數**選取**陳述式中的目前資料列集的最後一個資料列的值，然後執行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此陳述式會在 「 客戶 」 資料表中建立第二個結果集，其中是原始的結果集-下一個資料列集在此情況下的第一個資料列集的資料列集。 資料指標會傳回這個資料列集，應用程式。  
  
 有趣的是要注意這種方式實作的動態資料指標實際上會建立許多的結果集，以允許它偵測到原始的結果集的變更。 應用程式永遠不會了解這些輔助結果集; 存在它只會出現如資料指標能夠偵測到原始的結果集的變更。
