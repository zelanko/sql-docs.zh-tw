---
title: 參數資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: 5140c69184332b1760859421b7e802a5163a0f09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100600"
---
# <a name="parameter-data-types"></a>參數資料類型
雖然以**SQLBindParameter**指定的每個參數都是使用 sql 資料類型來定義的，但 sql 語句中的參數沒有內部資料類型。 因此，只有在語句中的資料類型可以從另一個運算元推斷時，才可以將參數標記包含在 SQL 語句中。 例如，在算術運算式中，例如？ + COLUMN1，參數的資料型別可以從 COLUMN1 所代表之命名資料行的資料型別推斷而來。 如果無法判斷資料類型，應用程式就無法使用參數標記。  
  
 下表描述根據 SQL-92，如何判斷數種參數類型的資料類型。 如需使用其他 SQL 子句時推斷參數類型的更完整規格，請參閱 SQL-92 規格。  
  
|參數的位置|假設的資料類型|  
|---------------------------|-----------------------|  
|二元算術或比較運算子的一個運算元|與另一個運算元相同|  
|**BETWEEN**子句中的第一個運算元|與第二個運算元相同|  
|**BETWEEN**子句中的第二個或第三個運算元|與第一個運算元相同|  
|**在中**搭配使用的運算式|與第一個值或子查詢的 [結果] 資料行相同|  
|**在中**搭配使用的值|與運算式相同，如果運算式中有參數標記，則為第一個值|  
|搭配**LIKE**使用的模式值|VARCHAR|  
|搭配**update**使用的更新值|與更新資料行相同|
