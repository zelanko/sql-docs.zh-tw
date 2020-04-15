---
title: ODBC 靜態游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282440"
---
# <a name="odbc-static-cursors"></a>ODBC 靜態資料指標
靜態游標是結果集顯示為靜態的游標。 它通常不會檢測打開游標后對結果集的成員身份、順序或值所做的更改。 例如,假設靜態游標獲取一行,然後另一個應用程式更新該行。 如果靜態游標重新提取行,則它看到的值將保持不變,儘管其他應用程序進行了更改。  
  
 靜態游標可以檢測自己的更新、刪除和插入,儘管它們不需要這樣做。 特定靜態游標是否檢測到這些更改將通過**SQLGetInfo**中的SQL_STATIC_SENSITIVITY選項進行報告。 靜態游標永遠不會檢測到其他更新、刪除和插入。  
  
 SQL_ATTR_ROW_STATUS_PTR語句屬性指定的行狀態陣列可以包含任何行的SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO或SQL_ROW_ERROR。 它返回SQL_ROW_UPDATED、SQL_ROW_DELETED或SQL_ROW_ADDED,用於游標更新、刪除或插入的行,前提是游標可以檢測到此類更改。  
  
 靜態游標通常是通過鎖定結果集中的行或複製結果集或快照實現的。 儘管鎖定行相對容易操作,但它有顯著減少併發的缺點是顯著減少併發性。 製作副本允許更大的併發性,並允許游標通過修改副本來跟蹤其自己的更新、刪除和插入。 但是,複製的製作成本更高,並且可能會由於其他數據被其他人更改而偏離基礎數據。
