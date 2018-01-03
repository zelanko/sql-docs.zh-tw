---
title: "擷取結果 （基本） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0762d7f70becf8c6bdbd86bee524bc964676f59
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="retrieving-results-basic"></a>擷取結果 （基本）
A*結果集*是一組符合特定準則的資料來源上的資料列。 它是概念性的資料表，從查詢結果，且應用程式可使用以表格形式。 **選取**陳述式、 目錄函數和一些程序建立結果集。 在下列範例中，第一個 SQL 陳述式會建立包含所有資料列和 「 訂單 」 資料表中的所有資料行的結果集和第二個 SQL 陳述式會建立包含訂單、 銷售人員，以及狀態資料行 Orders 資料表中資料列的結果集中的狀態為開啟：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果集可以是空的這是不同的結果集隨時。 例如，下列 SQL 陳述式會建立空的結果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空的結果集並無不同之處在於它沒有任何資料列集的其他結果。 例如，應用程式可以擷取結果集的中繼資料，可以嘗試提取資料列，和必須關閉資料指標結果集。  
  
 從資料來源擷取資料列，然後將其傳回至應用程式的程序稱為*擷取*。 本章節將說明該程序的基本部分。 如需更進階的主題，例如區塊和可捲動資料指標，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)和[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需更新的相關資訊，刪除和插入資料列，請參閱[更新資料概觀](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [已建立結果集了嗎？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [繫結資料行](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [擷取資料](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)
