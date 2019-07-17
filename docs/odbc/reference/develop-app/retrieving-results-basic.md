---
title: 擷取結果 （基本） |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020476"
---
# <a name="retrieving-results-basic"></a>擷取結果 (基本)
A*結果集*是一組符合特定準則的資料來源上的資料列。 它是概念性的資料表所產生的查詢及表格式格式，是可為應用程式。 **選取**陳述式、 目錄函數和一些程序建立結果集。 在下列範例中，第一個 SQL 陳述式會建立包含所有資料列和 「 訂單 」 資料表中的所有資料行的結果集，和第二個 SQL 陳述式會建立包含 「 訂單 」 資料表中的資料列的 OrderID、 銷售人員，以及狀態資料行的結果集以狀態為開啟：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果集可以是空的這是從沒有完全設定的結果不同。 例如，下列 SQL 陳述式會建立空的結果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空的結果集並無不同之處在於它沒有任何資料列集的其他結果。 例如，應用程式可以擷取結果集的中繼資料，可以嘗試提取資料列，和必須關閉資料指標結果集。  
  
 從資料來源擷取資料列，並將其傳回至應用程式的程序會呼叫*擷取*。 本章節將說明該程序的基本部分。 如需更進階的主題，例如區塊和可捲動資料指標，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)並[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需詳細資訊更新、 刪除和插入資料列，[更新資料概觀](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [已建立結果集了嗎？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [繫結資料行](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [擷取資料](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)
