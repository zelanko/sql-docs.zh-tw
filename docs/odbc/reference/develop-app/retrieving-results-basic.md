---
title: 正在抓取結果（基本） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020476"
---
# <a name="retrieving-results-basic"></a>擷取結果 (基本)
*結果集*是一組資料來源上符合特定準則的資料列。 它是查詢所產生的概念資料表，可用於表格式表單中的應用程式。 **SELECT**語句、目錄函數和一些程式會建立結果集。 在下列範例中，第一個 SQL 語句會建立包含 Orders 資料表中所有資料列和所有資料行的結果集，而第二個 SQL 語句會建立結果集，其中包含 Orders 資料表中之資料列的「訂單」、「銷售人員」和「狀態」資料行。其狀態為 [開啟]：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果集可以是空的，這與完全沒有的結果集不同。 例如，下列 SQL 語句會建立空的結果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空的結果集與其他任何結果集並無不同，但沒有任何資料列。 例如，應用程式可以抓取結果集的中繼資料，可以嘗試提取資料列，而且必須關閉結果集上的資料指標。  
  
 從資料來源中抓取資料列，並將其傳回給應用程式的過程稱為「*提取*」。 本節說明該程式的基本部分。 如需更多 advanced 主題的相關資訊，例如區塊和可滾動的資料指標，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)和可[滾動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需有關更新、刪除和插入資料列的詳細資訊，請參閱[更新資料總覽](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [已建立結果集了嗎？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [繫結資料行](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [擷取資料](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)
