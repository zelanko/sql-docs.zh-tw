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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f94b83ef1458cd9f8368d1bea3a39682bd80b1a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302320"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動態資料指標
動態資料指標只是： dynamic。 它可以偵測到資料指標開啟後，對結果集的成員資格、順序和值所做的任何變更。 例如，假設動態資料指標擷取兩個資料列，而其他應用程式接著更新其中一個資料列並刪除另一個資料列。 如果動態資料指標接著嘗試重新擷取這些資料列，它就不會找到已刪除的資料列，而是會傳回已更新資料列的新值。  
  
 動態資料指標會偵測所有的更新、刪除和插入，同時也會偵測到它們自己和其他人所做的動作。 （這取決於交易的隔離等級，如 SQL_ATTR_TXN_ISOLATION 連接屬性所設定）。SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的資料列狀態陣列會反映這些變更，而且可以包含 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 因為動態資料指標不會傳回資料列集以外的已刪除資料列，因此無法再將其傳回資料列狀態陣列中的已刪除資料列或其對應元素，因此無法傳回 SQL_ROW_DELETED。 只有在呼叫**SQLSetPos**更新資料列，而不是由另一個資料指標更新時，才會傳回 SQL_ROW_ADDED。  
  
 在資料庫中執行動態資料指標的其中一種方式，是建立定義結果集之成員資格和排序的選擇性索引。 因為索引會在其他專案進行變更時進行更新，所以以這類索引為基礎的資料指標會受到所有變更的影響。 藉由在索引中進行處理，可以在這個索引所定義的結果集中進行額外的選擇。  
  
 藉由要求以唯一索引鍵來排序結果集，可以模擬動態資料指標。 有了這種限制，每次資料指標提取資料列時，就會執行**SELECT**語句來進行提取。 例如，假設結果集是由這個語句所定義：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要提取此結果集中的下一個資料列集，模擬的資料指標會將下列**SELECT**語句中的參數設定為目前資料列集最後一列中的值，然後執行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 這個語句會建立第二個結果集，第一個資料列集是原始結果集中的下一個資料列集，在此案例中是 Customers 資料表中的資料列集。 游標會將此資料列集傳回到應用程式。  
  
 值得注意的是，以這種方式執行的動態資料指標實際上會建立許多結果集，讓它能夠偵測到原始結果集的變更。 應用程式永遠不會學習這些輔助結果集的存在與否;它就像資料指標能夠偵測到原始結果集的變更一樣。
