---
title: 參數標記 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303569"
---
# <a name="parameter-markers"></a>參數標記
根據 SQL-92 規範,應用程式不能在以下位置放置參數標記。 有關更全面的清單,請參閱 SQL-92 規範。  
  
-   在**SELECT**清單中  
  
-   作為*比較謂詞*中的兩個*運算式*  
  
-   為二進位運算子的兩個操作數  
  
-   建立**式建立中的建立的建立的建立的建立的操作**  
  
-   作為**BETWEEN**操作的第一個和第三個操作數  
  
-   為**IN**操作的表示式和第一個值  
  
-   為一個一元 + 或 - 操作的操作  
  
-   為*集函數引用*的參數  
  
 有關參數標記的詳細資訊,請參閱 SQL-92 規範。 有關參數的詳細資訊,請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
