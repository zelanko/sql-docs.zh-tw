---
title: 目錄功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb28ec6f4ea299dae8737fc707fd53e4d102442d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305199"
---
# <a name="catalog-functions"></a>目錄函式
所有資料庫都有一個結構,用於概述數據在資料庫中的存儲方式。 例如,簡單的銷售訂單資料庫可能具有下圖中所示的結構,其中 ID 列用於連結表。  
  
 ![顯示簡單資料庫的結構](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 此結構與其他資訊(如特權)儲存在一組稱為資料庫目錄的系統表中 *,* 則稱為*資料字典*。  
  
 應用程式可以通過調用*目錄函數*來發現此結構。 目錄函數返回結果集中的資訊,通常通過針對目錄中的表的**SELECT**語句實現。 例如，應用程式可能要求的結果集包含系統上所有資料表，或是特定資料表中所有資料行的相關資訊。  
  
 此章節包含下列主題。  
  
-   [使用目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [ODBC 中的目錄函式](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
