---
title: sp_OAMethod (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ef5d79a14aaee0b8f23738c3e359e37032d80318
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260804"
---
# <a name="spoamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  呼叫 OLE 物件的方法。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>引數  
 *objecttoken*  
 使用先前建立的 OLE 物件的物件 token **sp_OACreate**。  
  
 *方法名稱*  
 這是要呼叫之 OLE 物件的方法名稱。  
  
 *returnvalue***輸出**  
 這是 OLE 物件的方法傳回值。 如果指定的話，它必須是適當資料類型的本機變數。  
  
 如果此方法傳回單一值，也可以指定一個本機變數*returnvalue*，它會傳回此方法傳回值，在本機變數，或不指定*returnvalue*，它會傳回方法會傳回做為單一資料行、 單一資料列結果集給用戶端的值。  
  
 如果此方法傳回的值不是 OLE 物件， *returnvalue*必須是資料類型的本機變數**int**。物件 Token 儲存在本機變數中，這個物件 Token 可以搭配其他 OLE Automation 預存程序來使用。  
  
 當方法傳回值是陣列，如果*returnvalue*指定，則設定為 NULL。  
  
 當發生下列中的任何狀況時，都會產生錯誤：  
  
-   *returnvalue*指定，但方法不會傳回值。  
  
-   方法傳回含有超出二維的陣列。  
  
-   方法在輸出參數中傳回陣列。  
  
 [  *@parametername* * * =**]*參數*[**輸出**]  
 這是一個方法參數。 如果指定，*參數*必須是適當的資料類型的值。  
  
 若要取得輸出參數，傳回值*參數*必須是適當資料類型的本機變數和**輸出**必須指定。 如果指定常數參數，或如果**輸出**未指定，任何傳回輸出參數的值會被忽略。  
  
 如果指定， *parametername*必須是名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]具名參數。 請注意，  **@** *parametername*不[!INCLUDE[tsql](../../includes/tsql-md.md)]本機變數。@ 記號 (**@ * *) 會移除和*parametername*傳遞給 OLE 物件做為參數名稱。 您必須在指定好所有位置性參數之後，指定所有具名參數。  
  
 *n*  
 這是一個預留位置，表示可以指定多個參數。  
  
> [!NOTE]  
>  *@parametername* 可以是具名的參數，因為它是指定方法的一部分，並且會傳遞至物件。 這個預存程序的其他參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需有關 HRESULT 傳回碼[OLE Automation 傳回碼與錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>結果集  
 如果方法傳回值是含有一或兩個維度的陣列，就會將陣列傳回用戶端作為結果集：  
  
-   一維陣列會以單一資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。 換言之，這個陣列是以 (columns) 的方式傳回。  
  
-   二維陣列會以多資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。資料行數目等於陣列第一維的元素數目，資料列數目等於陣列第二維的元素數目。 換言之，這個陣列是以 (columns, rows) 的方式傳回。  
  
 當屬性傳回值或方法傳回值是否為陣列、 **sp_OAGetProperty**或**sp_OAMethod**結果集傳回給用戶端。 (方法輸出參數不能是陣列。)這些程序會掃描陣列中的所有資料值來判斷適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，以及結果集中每個資料行所用的資料長度。 對於特定資料行，這些程序會利用資料類型和長度來表示這個資料行中的所有資料值。  
  
 當資料行中的所有資料值都共用相同的資料類型時，整個資料行都會使用這個資料類型。 當資料行中的資料值是不同資料類型時，便會根據下表來選擇整個資料行的資料類型。  
  
||int|float|money|datetime|varchar|nvarchar|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>備註  
 您也可以使用**sp_OAMethod**取得屬性值。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-a-method"></a>A. 呼叫方法  
 下列範例會呼叫`Connect`先前建立的方法**SQLServer**物件。  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. 取得屬性  
 下列範例會取得`HostName`屬性 (先前建立**SQLServer**物件) 並將它儲存在區域變數中。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
