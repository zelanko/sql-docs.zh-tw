---
title: 檢索結果(基本) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304329"
---
# <a name="retrieving-results-basic"></a>擷取結果 (基本)
*結果集*是數據源上的一組與特定條件匹配的行。 它是一個概念表,由查詢生成,並且可用於表格形式的應用程式。 **選擇**語句、目錄函數和某些過程將創建結果集。 在下面的範例中,第一個 SQL 語句建立一個結果集,其中包含「訂單」表中的所有行和所有列,第二個 SQL 語句為狀態為 OPEN 的「訂單」表中的行創建一個結果集:在「狀態為打開」的「訂單」表中,這些行包含 OrderID、SalesPerson 和狀態列:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果集可以為空,這與沒有結果集完全不同。 例如,以下 SQL 語句建立一個空結果集:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空結果集與任何其他結果集沒有什麼不同,只是它沒有行。 例如,應用程式可以檢索結果集的元數據,可以嘗試提取行,並且必須關閉結果集上的游標。  
  
 從資料來源檢索行並將其傳回到應用程式的過程為*擷取*。 本節介紹該過程的基本部分。 有關更進階主題(如區塊和可捲軸游標)的資訊,請參閱[區塊游標](../../../odbc/reference/develop-app/block-cursors.md)與[可捲動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有關更新、刪除與插入行的資訊,請參考[更新資料概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [已建立結果集了嗎？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [繫結資料行](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [擷取資料](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)
