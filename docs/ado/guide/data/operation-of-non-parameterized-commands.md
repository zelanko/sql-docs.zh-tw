---
title: 非參數化命令的作業 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3512b484425749ed027f6533dab7398765c1af2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924742"
---
# <a name="operation-of-non-parameterized-commands"></a>非參數化命令的作業
所有提供者命令執行的非參數化命令，而**資料錄集**命令執行期間所建立。 如果此命令會以同步方式執行所有**資料錄集**會完全擴展。 如果選取的非同步擴展模式，填入的狀態**資料錄集**母體擴展的模式和大小而定**資料錄集**。  
  
 例如，*父命令*可能會傳回**資料錄集**的 Customers 資料表中，從公司的客戶和*子命令*可能會傳回**資料錄集**的 Orders 資料表中的所有客戶的訂單。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 若是非參數化父-子關聯性，每個父系和子系**資料錄集**物件必須具有在一般用來建立關聯的資料行。 在 RELATE 子句中，命名資料行*父資料行*第一次，然後*子資料行*。 資料行可能會有不同的名稱，在其各自**資料錄集**物件，但若要指定有意義的關聯性必須參考相同的資訊。 例如，**客戶**並**訂單資料錄集**物件兩者都可能會有 customerID 欄位。 因為子系的成員資格**Recordset**取決於提供者命令中，子系**資料錄集**可以包含被遺棄的資料列。 不含其他重整，這些被遺棄的資料列都無法存取。  
  
 資料成形將的章節資料行附加至父代**資料錄集**。 章節資料行中的值為子系中的資料列參考**資料錄集**，其滿足 RELATE 子句。 也就是相同的值會處於*父資料行*指定的父資料列中的*子資料行*章子系的所有資料列。 當多個 TO 子句相同的 RELATE 子句中使用時，它們會以隱含方式結合使用 AND 運算子。 如果在 RELATE 子句中的父資料行並不會構成父系的索引鍵**資料錄集**，單一子資料列可以有多個父資料列。  
  
 當您存取的章節資料行中的參考時，ADO 會自動擷取**資料錄集**參考所表示。 請注意，在非參數化命令中，雖然將整個子**資料錄集**已擷取，本章只會呈現的資料列子集。  
  
 如果附加的資料行沒有任何*章別名*，自動為它會產生名稱。 A[欄位](../../../ado/reference/ado-api/field-object.md)物件中的資料行都會附加至**資料錄集**物件的[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合和其資料型別會**adChapter**.  
  
 如需有關瀏覽階層式資訊**Recordset**，請參閱[存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
