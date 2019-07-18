---
title: 物件階層語法 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3405621d604e6450756520f6d93b66a51d4d66c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941980"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>物件階層語法 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  *Propertyname* sp_OAGetProperty 和 sp_OASetProperty 的參數與*methodname* sp_OAMethod 參數支援類似的物件階層語法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. 使用這個特殊語法時，這些參數具有下列一般格式。  
  
## <a name="syntax"></a>語法  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>引數  
 *J*  
 是在階層中的 OLE 物件*objecttoken*預存程序中所指定。 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 語法來指定一系列集合、物件屬性和傳回物件的方法。 這個系列中的每一個物件規範必須以句點 (.) 隔開。  
  
 這個系列中的項目可以是集合的名稱。 請使用這個語法來指定集合：  
  
 集合 ("*項目*")  
  
 需要雙引號 (")。 集合的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 驚嘆號 (!) 語法不受支援。  
  
 *PropertyOrMethod*  
 屬性的名稱或泛型方法的*Traversedobject&lt*。  
  
 若要使用 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 參數 (包括 sp_OAMethod 輸出參數的支援)，來指定所有索引或方法參數，請使用下列語法：  
  
 *PropertyOrMethod*  
  
 若要在括號內指定所有索引或方法參數 (使 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 的所有索引或方法參數被忽略)，請使用下列語法：  
  
 *PropertyOrMethod*([ *ParameterName*: =]"*參數*"[，...])  
  
 需要雙引號 (")。 您必須在指定好所有位置性參數之後，指定所有具名參數。  
  
## <a name="remarks"></a>備註  
 如果*Traversedobject&lt*未指定，則*PropertyOrMethod*需要。  
  
 如果*PropertyOrMethod*未指定，則*j*從 OLE Automation 預存程序會傳回做為物件 token 輸出參數。 如果*PropertyOrMethod*指定時，屬性或方法*j*呼叫時，以及屬性值或方法傳回值做為輸出參數從傳回 OLE Automation預存程序。  
  
 如果任何項目*Traversedobject&lt*清單不會傳回 OLE 物件，則會引發錯誤。  
  
 如需有關 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE 物件語法的詳細資訊，請參閱 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 文件集。  
  
 如需有關 HRESULT 傳回碼的詳細資訊，請參閱 < [sp_OACreate &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 以下是使用 SQL-DMO SQLServer 物件之物件階層語法的範例。  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE Automation 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
