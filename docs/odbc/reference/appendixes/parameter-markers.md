---
title: 參數標記 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: acb8d5f9687798bc0efa514ee8646b16140fcd36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100578"
---
# <a name="parameter-markers"></a>參數標記
根據 SQL-92 規格中，應用程式無法將參數標記放在下列位置。 如需更完整的清單，請參閱 SQL-92 規格。  
  
-   在 **選取**清單  
  
-   為 雙向*運算式*在*比較述詞*  
  
-   當做二元運算子的兩個運算元  
  
-   做為的第一個和第二個運算元**BETWEEN**作業  
  
-   做為第一個和第三個運算元的**BETWEEN**作業  
  
-   當做運算式，而第一個值**IN**作業  
  
-   運算元是一元的 + 或-作業  
  
-   做為引數*集函式參考*  
  
 如需有關參數標記的詳細資訊，請參閱 SQL-92 規格。 如需有關參數的詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。
