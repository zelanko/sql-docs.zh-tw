---
title: "非參數化命令的作業 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a025cf381bdf5a51cb825294bf5a5399fc033b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="operation-of-non-parameterized-commands"></a>非參數化命令的作業
對於非參數化命令，會執行所有的提供者命令和**資料錄集**命令執行期間所建立。 如果命令以同步方式，執行所有**資料錄集**會完全擴展。 如果選取非同步擴展模式，則填入的狀態**資料錄集**母體擴展模式和大小而定**資料錄集**。  
  
 例如，*父命令*可能會傳回**資料錄集**的客戶從 Customers 資料表中，公司和*子命令*可能會傳回**資料錄集**的 Orders 資料表中的所有客戶的訂單。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 針對非參數化父子式關聯性，每個父和子**資料錄集**物件必須具有在一般用來建立其關聯的資料行。 在 RELATE 子句中，命名資料行*父資料行*第一次，然後*子資料行*。 資料行可能會有不同的名稱，在其各自**資料錄集**物件，但若要指定有意義的關聯性必須參考相同的資訊。 例如，**客戶**和**訂單資料錄集**物件兩者都可能會有 customerID 欄位。 因為子系的成員資格**資料錄集**取決於提供者命令中，子**資料錄集**可以包含被遺棄的資料列。 沒有其他才可遏制，這些被遺棄的資料列都無法存取。  
  
 將資料成形附加至父代的章節資料行**資料錄集**。 章節資料行中的值是子系中的資料列的參考**資料錄集**，其滿足 RELATE 子句。 也就是說，相同的值是在*父資料行*在指定的父資料列的*子資料行*章子系的所有資料列。 當多個 TO 子句相同 RELATE 子句中使用時，會隱含地合併使用 AND 運算子。 如果在 RELATE 子句中的父資料行不會形成父系的索引鍵**資料錄集**，一個子資料列可以有多個父資料列。  
  
 當您存取章節資料行中的參考時，ADO 會自動擷取**資料錄集**參考所表示。 請注意，在非參數化命令中，雖然整個子系**資料錄集**已擷取，章只會呈現資料列的子集。  
  
 如果附加的資料行沒有任何*章別名*，自動為它會產生名稱。 A[欄位](../../../ado/reference/ado-api/field-object.md)物件資料行就會附加至**資料錄集**物件的[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合和其資料類型會是**adChapter**.  
  
 如需有關瀏覽階層式資訊**資料錄集**，請參閱[存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
