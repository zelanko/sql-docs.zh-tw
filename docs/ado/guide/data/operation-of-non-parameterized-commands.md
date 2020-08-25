---
description: 非參數化命令的作業
title: 非參數化命令的操作 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b0f425deb87e831547d24a4b81f7d1a601e344a
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805668"
---
# <a name="operation-of-non-parameterized-commands"></a>非參數化命令的作業
針對非參數化命令，會執行所有提供者命令，並在命令執行期間建立 **記錄集** 。 如果命令是以同步方式執行，則會完整填入所有 **記錄集** 。 如果選取了非同步擴展模式，則 **記錄集** 的填入狀態將取決於擴展模式和 **記錄集**的大小。  
  
 例如， *父系命令* 可能會從 customers 資料表傳回公司客戶的 **記錄集** ，而 *子命令* 可能會傳回 orders 資料表中所有客戶的訂單 **記錄集** 。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 如果是非參數化的父子式關聯性，每個父系和子 **記錄集** 物件都必須有共同的資料行，才能將它們相關聯。 這些資料行會在 [關聯性] 子句、[ *父資料行* ] 和 [ *子資料行*] 中命名。 這些資料行在各自的 **記錄集** 物件中可能會有不同的名稱，但必須參考相同的資訊，才能指定有意義的關聯性。 例如， **Customers** 和 **Orders 記錄集** 物件可以有 customerID 欄位。 因為子 **記錄集** 的成員資格是由提供者命令所決定，所以子 **記錄集** 可以包含孤立的資料列。 這些孤立的資料列無法存取，而不需要額外的重構。  
  
 資料成形會將章節資料行附加至父 **記錄集**。 [章節] 資料行中的值是子 **記錄集中**資料列的參考，可滿足關聯子句。 也就是說，相同的值會在給定父資料 *列的父* 資料行中，如同在章節子系的所有資料列的 *子* 資料行中一樣。 當在相同的關聯子句中使用多個 TO 子句時，它們會使用 AND 運算子來隱含地結合。 如果關聯子句中的父資料行不構成父 **記錄集**的索引鍵，則單一子資料列可以有多個父資料列。  
  
 當您存取章節資料行中的參考時，ADO 會自動抓取參考所表示的 **記錄集** 。 請注意，在非參數化命令中，雖然已抓取整個子 **記錄集** ，但該章節只會顯示資料列的子集。  
  
 如果附加的資料行沒有 *章節別名*，就會自動產生名稱。 資料行的 [欄位](../../reference/ado-api/field-object.md) 物件將會附加至 **記錄集** 物件的 [Fields](../../reference/ado-api/fields-collection-ado.md) 集合，而且其資料類型將會是 **adChapter**。  
  
 如需導覽階層式 **記錄集**的詳細資訊，請參閱 [存取階層式記錄](./accessing-rows-in-a-hierarchical-recordset.md)集中的資料列。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](./data-shaping-example.md)   
 [正式式圖形文法](./formal-shape-grammar.md)   
 [一般 Shape 命令](./shape-commands-in-general.md)