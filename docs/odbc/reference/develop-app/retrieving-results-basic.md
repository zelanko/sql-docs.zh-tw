---
description: 擷取結果 (基本)
title: " (基本) 抓取結果 |Microsoft Docs"
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
ms.openlocfilehash: a43064703e7ee448de89396135fa610e972e2679
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461360"
---
# <a name="retrieving-results-basic"></a>擷取結果 (基本)
*結果集*是資料來源上符合特定準則的一組資料列。 它是查詢所產生的概念資料表，可供表格形式的應用程式使用。 **SELECT** 語句、目錄函數和某些程式會建立結果集。 在下列範例中，第一個 SQL 語句會建立結果集，其中包含 Orders 資料表中的所有資料列和所有資料行，而第二個 SQL 語句會建立結果集，其中包含狀態開啟之 Orders 資料表中資料列的 [訂單]、[銷售人員] 和 [狀態] 資料行：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果集可以是空的，而且完全不會與任何結果集相同。 例如，下列 SQL 語句會建立空的結果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空白的結果集與其他任何結果集並無不同，差別在於它沒有任何資料列。 例如，應用程式可以取出結果集的中繼資料，可以嘗試提取資料列，而且必須將資料指標關閉到結果集上。  
  
 從資料來源中取出資料列並將其傳回給應用程式的程式稱為「 *提取*」。 本節說明該流程的基本部分。 如需更多 advanced 主題的相關資訊，例如區塊和可滾動的資料指標，請參閱 [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md) 和可滾動的資料 [指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需有關更新、刪除和插入資料列的詳細資訊，請參閱 [更新資料總覽](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [已建立結果集了嗎？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [繫結資料行](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [提取資料](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)
