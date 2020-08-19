---
description: 參數資料類型
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
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 0114f0cff269d35ddf1e93c653c46bcc8d863a29
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483241"
---
# <a name="parameter-data-types"></a>參數資料類型
即使以 **SQLBindParameter** 指定的每個參數都是使用 sql 資料類型來定義，但是 SQL 語句中的參數沒有內建資料類型。 因此，只有在語句中的其他運算元可以推斷出其資料類型時，才可以將參數標記包含在 SQL 語句中。 例如，在像是的算術運算式中？ + COLUMN1，可以從 COLUMN1 所代表之命名資料行的資料類型推斷參數的資料類型。 如果無法判斷資料類型，應用程式就無法使用參數標記。  
  
 下表說明如何根據 SQL-92，判斷資料類型的數種類型的參數。 如需使用其他 SQL 子句時推斷參數類型的更完整規格，請參閱 SQL-92 規格。  
  
|參數的位置|假設的資料類型|  
|---------------------------|-----------------------|  
|二元算術或比較運算子的一個運算元|與另一個運算元相同|  
|**BETWEEN**子句中的第一個運算元|與第二個運算元相同|  
|**BETWEEN**子句中的第二個或第三個運算元|與第一個運算元相同|  
|搭配 **使用的運算式**|與第一個值或子查詢的結果資料行相同|  
|**在中**搭配使用的值|和運算式相同，如果運算式中有參數標記，則為第一個值|  
|搭配**LIKE**使用的模式值|VARCHAR|  
|搭配**update**使用的更新值|與更新資料行相同|
