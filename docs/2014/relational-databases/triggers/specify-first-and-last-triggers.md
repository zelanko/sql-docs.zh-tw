---
title: 指定第一個與最後一個觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8badfd8ab7fc149ddce797f6aeb33ac896dc1e51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133908"
---
# <a name="specify-first-and-last-triggers"></a>指定第一個與最後一個觸發程序
  您可以指定與資料表關聯的其中一個 AFTER 觸發程序，做為針對每一個 INSERT、DELETE 和 UPDATE 觸發動作而引發的第一個或最後一個 AFTER 觸發程序。 在第一個及最後一個觸發程序之間啟動的 AFTER 觸發程序，會以未定義的順序執行。  
  
 若要指定 AFTER 觸發程序的順序，請使用 **sp_settriggerorder** 預存程序。 **sp_settriggerorder** 具有下列選項。  
  
|選項|描述|  
|------------|-----------------|  
|**第一個**|指定 DML 觸發程序為針對觸發動作而引發的第一個 AFTER 觸發程序。|  
|**最後一個**|指定 DML 觸發程序為針對觸發動作而引發的最後一個 AFTER 觸發程序。|  
|**無**|指定 DML 觸發程序的引發並無特定的順序。 主要用來重設第一個或最後一個觸發程序。|  
  
 下列範例示範如何使用 **sp_settriggerorder**：  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  第一個及最後一個觸發程序，必須是兩個不同的 DML 觸發程序。  
  
 可以同時對一個資料表定義 INSERT、UPDATE 及 DELETE 等觸發程序。 每個陳述式類型都可以擁有它自己的第一個及最後一個觸發程序，但它們不得為相同的觸發程序。  
  
 如果針對某資料表定義的第一個或最後一個觸發程序並不涵蓋觸發動作，例如未涵蓋 FOR UPDATE、FOR DELETE 或 FOR INSERT，則遺漏的動作不會有第一個或最後一個觸發程序。  
  
 INSTEAD OF 觸發程序不得被指定為第一個或最後一個觸發程序。 INSTEAD OF 觸發程序必須在更新基礎資料表之前啟動。 如果是由 INSTEAD OF 觸發程序更新基礎資料表，則更新會發生在引發對資料表定義的 AFTER 觸發程序之前。 例如，如果在檢視上的 INSTEAD OF INSERT 觸發程序將資料插入基底資料表，而基底資料表本身包含 INSTEAD OF INSERT 觸發程序和三個 AFTER INSERT 觸發程序，就會引發基底資料表上的 INSTEAD OF INSERT 觸發程序，而不是插入動作，而且在基底資料表上的任何插入動作之後，都會引發基底資料表的 AFTER 觸發程序。 如需詳細資訊，請參閱 [DML Triggers](dml-triggers.md)。  
  
 如果 ALTER TRIGGER 陳述式變更第一個或最後一個觸發程序，則會捨棄 **First** 或 **Last** 屬性，並且將順序值設為 [None]。 順序必須使用 **sp_settriggerorder** 進行重設。  
  
 OBJECTPROPERTY 函數也會利用 **ExecIsFirstTrigger** 及 **ExecIsLastTrigger**屬性，來報告觸發程序究竟是第一個或最後一個觸發程序。  
  
 複寫會為包含在即時更新或佇列式更新訂閱的資料表，自動產生第一個觸發程序。 複寫需要觸發程序是第一個觸發程序。 當您嘗試將含有第一個觸發程序的資料表包括在立即更新或佇列更新訂閱中，複寫會引發錯誤。 如果您嘗試在資料表已加入訂閱後，將觸發程序變成第一個觸發程序，則 **sp_settriggerorder** 會傳回錯誤。 如果您對複寫觸發程序使用 ALTER，或使用 **sp_settriggerorder** 將複寫觸發程序變更為最後一個或無觸發程序，則訂閱將無法正常運作。  
  
## <a name="see-also"></a>另請參閱  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql)  
  
  
