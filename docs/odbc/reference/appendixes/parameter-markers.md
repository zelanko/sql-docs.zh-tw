---
title: 參數標記 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df895c9e9956c1fde178824d1e14030246710946
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers"></a>參數標記
根據 sql-92 規格，應用程式無法將參數標記放在下列位置中。 如需更完整清單，請參閱 sql-92 規格。  
  
-   在**選取**清單  
  
-   兩者*運算式*中*比較述詞*  
  
-   當做二元運算子的兩個運算元  
  
-   第一個和第二個運算元為**BETWEEN**作業  
  
-   做為第一個和第三個運算元的**BETWEEN**作業  
  
-   當做運算式，而第一個值**IN**作業  
  
-   一元的運算元為 + 或 – 作業  
  
-   做為引數*組函式參考*  
  
 如需參數標記的詳細資訊，請參閱 sql-92 規格。 如需參數的詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。
