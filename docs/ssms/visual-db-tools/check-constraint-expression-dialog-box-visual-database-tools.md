---
title: 檢查條件約束運算式對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0c35a5a617e02eba27e608668117da8856f720d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090775"
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>檢查條件約束運算式對話方塊 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
當附加檢查條件約束至資料表或資料行時，必須包含 SQL 運算式。 在提供的方塊中輸入檢查條件約束運算式。  
  
## <a name="uielement-list"></a>UIElement 清單  
運算式  
輸入運算式  
  
您可以建立簡單的條件約束運算式以檢查簡單條件的資料，或是可以建立使用布林運算子的複雜運算式，檢查數種條件的資料。 例如，假設 authors 資料表有 zip 資料行，而其中需要 5 位數的字串。 這個簡單的條件約束運算式保證只會允許 5 位數的資料：  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
或者，假設銷售資料表有名為 qty 的資料行，該資料航需要大於 0 的值。 這個簡單的條件約束保證只會允許正值：  
  
```  
qty > 0  
```  
  
或假設 orders 資料表限制所有信用卡訂單所接受的信用卡類型。 則這個範例條件約束保證如果是使用信用卡進行訂購，則只接受 Visa、MasterCard 或 American Express：  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>若要定義條件約束運算式  
在屬性頁面的 [檢查條件約束] 索引標籤中，使用下列語法，在 [檢查條件約束運算式] 方塊中輸入運算式：  
  
<pre>{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]</pre>  
  
SQL 語法是由下列參數組成：  
  
|參數|Description|  
|-------------|---------------|  
|常數|常值，例如數值或字元資料。 字元資料必須使用單引號 (') 括起來。|  
|column_name|指定資料行。|  
|函數|內建函數。|  
|! 運算子之後|算術、位元、比較或字串運算子。|  
|與|使用於布林運算式中，用於連接兩個運算式。 當兩個運算式都是 true 時傳回結果。<br /><br />當 AND 和 OR 同時在陳述式中使用時，會先處理 AND。 您可以使用括號來變更執行的順序。|  
|或|使用於布林運算式中，用於連接兩個條件。 當任一條件為 true 時，傳回結果。<br /><br />當 AND 和 OR 同時在陳述式中使用時，OR 是在 AND 之後進行檢驗。 您可以使用括號來變更執行的順序。|  
|NOT|否定任何布林運算式 (可以包括關鍵字，例如 LIKE、NULL、BETWEEN、IN 和 EXISTS)。<br /><br />當在陳述式中使用一個以上的邏輯運算子時，會首先處理 NOT。 您可以使用括號來變更執行的順序。|  
  
## <a name="see-also"></a>另請參閱  
[唯一條件約束與檢查條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
[建立唯一的條件約束](../../relational-databases/tables/create-unique-constraints.md)  
  
