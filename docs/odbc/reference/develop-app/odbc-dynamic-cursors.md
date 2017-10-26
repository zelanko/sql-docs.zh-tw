---
title: "ODBC 動態資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a60688231bc01f55cf5b49fae3bb8d6da4a54950
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-dynamic-cursors"></a>ODBC 動態資料指標
動態資料指標僅是： 動態。 它可以偵測到的成員資格、 順序和值之結果集資料指標開啟後所做的變更。 例如，假設動態資料指標擷取兩個資料列，並將另一個應用程式然後更新那些資料列的其中一個，並刪除其他。 如果動態資料指標會再嘗試重新提取這些資料列，它會找不到刪除的資料列，但會傳回更新的資料列的新值。  
  
 動態資料指標偵測所有更新，刪除與插入，同時其自己與其他人所完成。 （這受限於隔離等級的交易，所設定的 SQL_ATTR_TXN_ISOLATION 連接屬性。）將 sql_attr_row_status_ptr 設定陳述式屬性所指定之資料列狀態陣列會反映這些變更，而且可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO、 SQL_ROW_ERROR、 SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 因為動態資料指標不會傳回已刪除的資料列外資料列集，因此無法再識別結果集中刪除的資料列或資料列狀態陣列中相對應的元素存在，它不能傳回 SQL_ROW_DELETED。 透過呼叫來更新資料列時，才傳回 SQL_ROW_ADDED **SQLSetPos**、 由另一個資料指標進行更新時，不。  
  
 在資料庫中實作動態資料指標的一種方式所建立的選擇性索引定義成員資格，以及排序結果的設定。 當其他人進行變更時，會更新索引，因為根據這類索引的資料指標是機密的所有變更。 可以沿著索引處理額外的選取項目，此索引所定義的結果集內。  
  
 動態資料指標可以模擬透過要求的結果集來排序的唯一索引鍵。 這類限制提取會藉由執行**選取**陳述式每次資料指標提取資料列。 例如，假設結果集由這個陳述式所定義：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要擷取的下一步 在此結果集中的資料列集，模擬資料指標會設定的參數在下列**選取**陳述式中目前資料列集的最後一個資料列的值，然後執行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此陳述式會建立第二個結果集，其中第一個資料列集是原始結果集中的下一個資料列集 — 在此情況下，「 客戶 」 資料表中的資料列集。 資料指標會傳回至應用程式的這個資料列集。  
  
 值得注意這種方式實作的動態資料指標確實會建立多個結果集，可讓它偵測到原始的結果集的變更。 應用程式不會學習的這些輔助結果集存在它只會顯示如資料指標可以偵測到原始的結果集的變更。

