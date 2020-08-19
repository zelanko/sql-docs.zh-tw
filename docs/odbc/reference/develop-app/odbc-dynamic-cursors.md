---
description: ODBC 動態資料指標
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
ms.openlocfilehash: 19ae15a211329e07fdab13a5b6ff40e210e97cb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429190"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動態資料指標
動態資料指標就是：動態資料指標。 它可以偵測在開啟資料指標之後，對結果集的成員資格、順序和值所做的任何變更。 例如，假設動態資料指標擷取兩個資料列，而其他應用程式接著更新其中一個資料列並刪除另一個資料列。 如果動態資料指標接著嘗試重新擷取這些資料列，它就不會找到已刪除的資料列，而會傳回已更新資料列的新值。  
  
 動態資料指標會偵測它們自己和其他人所做的所有更新、刪除和插入。  (這會受限於 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級。 ) SQL_ATTR_ROW_STATUS_PTR 語句屬性指定的資料列狀態陣列反映這些變更，而且可以包含 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED 和 SQL_ROW_ADDED。 它無法傳回 SQL_ROW_DELETED，因為動態資料指標不會傳回資料列集以外的已刪除資料列，因此無法再辨識結果集內已刪除的資料列，或是資料列狀態陣列中的對應元素。 只有當 **SQLSetPos**的呼叫更新資料列時，不會傳回 SQL_ROW_ADDED，而是由另一個資料指標更新時才會傳回。  
  
 在資料庫中執行動態資料指標的其中一種方式是建立選擇性索引，以定義結果集的成員資格和順序。 因為當其他人進行變更時，索引會更新，所以以這類索引為基礎的資料指標會對所有變更有所區分。 藉由在索引中進行處理，可以在此索引所定義的結果集內進行其他選取。  
  
 藉由要求以唯一索引鍵來排序結果集，即可模擬動態資料指標。 有了這項限制，每次資料指標提取資料列時，就會執行 **SELECT** 語句來進行提取。 例如，假設結果集是由這個語句所定義：  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 若要提取此結果集內的下一個資料列集，模擬資料指標會將下列 **SELECT** 語句中的參數設定為目前資料列集最後一個資料列中的值，然後執行它：  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 這個語句會建立第二個結果集，第一個資料列集是原始結果集中的下一個資料列集，在此案例中為 Customers 資料表中的資料列集。 資料指標會將這個資料列集傳回給應用程式。  
  
 請注意，以這種方式執行的動態資料指標實際上會建立許多結果集，讓它能夠偵測對原始結果集的變更。 應用程式永遠不會學習這些輔助結果集是否存在;它看起來就像是資料指標能夠偵測到原始結果集的變更一樣。
