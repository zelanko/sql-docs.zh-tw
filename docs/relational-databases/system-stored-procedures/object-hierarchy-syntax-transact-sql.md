---
description: 物件階層語法 (Transact-SQL)
title: " (Transact-sql) 的物件階層語法 |Microsoft Docs"
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
ms.openlocfilehash: be02e82ef4ba1718f15bd083e3ffc3b86058a24b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498101"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>物件階層語法 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sp_OAGetProperty 和 sp_OASetProperty 的 *propertyname* 參數和 sp_OAMethod 的 *方法名稱* 參數支援類似的物件階層語法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 。 使用這個特殊語法時，這些參數具有下列一般格式。  
  
## <a name="syntax"></a>語法  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>引數  
 *TraversedObject*  
 這是在預存程式中指定之 *objecttoken* 下的階層中的 OLE 物件。 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 語法來指定一系列集合、物件屬性和傳回物件的方法。 這個系列中的每一個物件規範必須以句點 (.) 隔開。  
  
 這個系列中的項目可以是集合的名稱。 請使用這個語法來指定集合：  
  
 集合 ( "*item*" )   
  
 需要雙引號 (")。 集合的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 驚嘆號 (!) 語法不受支援。  
  
 *PropertyOrMethod*  
 這是 *TraversedObject*的屬性或方法的名稱。  
  
 若要使用 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 參數 (包括 sp_OAMethod 輸出參數的支援)，來指定所有索引或方法參數，請使用下列語法：  
  
 *PropertyOrMethod*  
  
 若要在括號內指定所有索引或方法參數 (使 sp_OAGetProperty、sp_OASetProperty 或 sp_OAMethod 的所有索引或方法參數被忽略)，請使用下列語法：  
  
 *PropertyOrMethod* ( [ *ParameterName*： =] "*parameter*" [，...] )   
  
 需要雙引號 (")。 您必須在指定好所有位置性參數之後，指定所有具名參數。  
  
## <a name="remarks"></a>備註  
 如果未指定 *TraversedObject* ，則需要 *PropertyOrMethod* 。  
  
 如果未指定 *PropertyOrMethod* ，則會以 OLE Automation 預存程式的物件標記輸出參數傳回 *TraversedObject* 。 如果指定 *PropertyOrMethod* ，則會呼叫 *TraversedObject* 的屬性或方法，並以 OLE Automation 預存程式的輸出參數傳回屬性值或方法傳回值。  
  
 如果 *TraversedObject* 清單中的任何專案沒有傳回 OLE 物件，則會引發錯誤。  
  
 如需有關 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE 物件語法的詳細資訊，請參閱 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 文件集。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱 [sp_OACreate &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列是使用 SQL-DMO SQLServer 物件之物件階層語法的範例。  
  
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
 [OLE Automation 範例腳本](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE Automation 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
