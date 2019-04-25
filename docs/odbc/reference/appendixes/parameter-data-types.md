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
manager: craigg
ms.openlocfilehash: e1f1097927f61355cf4a50f4287397d823fd3177
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632411"
---
# <a name="parameter-data-types"></a>參數資料類型
即使每個參數指定了**SQLBindParameter**會定義使用 SQL 資料類型，SQL 陳述式中的參數有沒有內建資料型別。 因此，參數標記可以包含在 SQL 陳述式才可以從陳述式中的另一個運算元推斷其資料類型。 例如，在這類的算術運算式嗎？ + COLUMN1，參數的資料型別可以從具名資料行 COLUMN1 所代表的資料型別推斷而來。 應用程式無法使用的參數標記，如果無法判別資料型別。  
  
 下表描述數種類型的參數，根據 SQL-92 如何判斷資料型別。 如需在其他 SQL 子句使用時，推斷參數類型的更完整規格，請參閱 SQL-92 規格。  
  
|參數的位置|假設資料類型|  
|---------------------------|-----------------------|  
|一個二元算術或比較運算子的運算元|另一個運算元相同|  
|中的第一個運算元**BETWEEN**子句|第二個運算元相同|  
|中的第二個或第三個運算元**BETWEEN**子句|第一個運算元相同|  
|搭配使用的運算式**IN**|第一個值或子查詢的結果資料行相同|  
|值，搭配**IN**|運算式或運算式中的參數標記時的第一個值相同|  
|模式值搭配**等**|VARCHAR|  
|搭配使用的更新值**更新**|更新資料行相同|
