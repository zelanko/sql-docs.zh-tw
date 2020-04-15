---
title: ODBC動態游標 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302320"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 動態資料指標
動態游標就是:動態。 它可以檢測打開游標后對結果集的成員身份、順序和值所做的任何更改。 例如，假設動態資料指標擷取兩個資料列，而其他應用程式接著更新其中一個資料列並刪除另一個資料列。 如果動態游標然後嘗試重新提取這些行,它將找不到已刪除的行,但將返回更新行的新值。  
  
 動態游標檢測所有更新、刪除和插入,包括它們自己和他人所做的更新。 (這受事務的隔離級別的約束,由SQL_ATTR_TXN_ISOLATION連接屬性設置。SQL_ATTR_ROW_STATUS_PTR語句屬性指定的行狀態陣列反映這些更改,可以包含SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO、SQL_ROW_ERROR、SQL_ROW_UPDATED和SQL_ROW_ADDED。 它不能返回SQL_ROW_DELETED,因為動態游標不會返回行集外的已刪除行,因此不再識別結果集中的已刪除行或其相應元素在行狀態陣列中是否存在。 僅當對**SQLSetPos**的調用更新行時,才會返回SQL_ROW_ADDED,而不是由另一個游標更新時返回該行。  
  
 在資料庫中實現動態游標的一種方法是創建一個選擇性索引,用於定義結果集的成員身份和順序。 由於當其他人進行更改時,索引會更新,因此基於此類索引的游標對所有更改都敏感。 通過沿索引處理,可以在此索引定義的結果集中進行其他選擇。  
  
 可以通過要求由唯一鍵排序結果集來類比動態游標。 在此類限制下,每次游標獲取行時,都會通過執行**SELECT**語句進行提取。 例如,假設結果集由以下語句定義:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 要取得此結果集中的下一個行集,模擬游標將以下**SELECT**語句中的參數設定為目前的行集最後一行中的值,然後執行它:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 此語句創建第二個結果集,其中第一個行集是原始結果集中的下一個行集 -在這種情況下,是客戶表中的行集。 游標將此行集返回到應用程式。  
  
 值得注意的是,以這種方式實現的動態游標實際上創建了許多結果集,從而可以檢測對原始結果集的更改。 應用程式從不瞭解這些輔助結果集的存在;它只是顯示,如果游標能夠檢測對原始結果集的更改。
