---
description: sp_OAMethod (Transact-SQL)
title: sp_OAMethod (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 98e487f2393aba0c33f91fba6a41dd096cb61368
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493101"
---
# <a name="sp_oamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
 這是先前使用 **sp_OACreate**所建立之 OLE 物件的物件 token。  
  
 *methodname*  
 這是要呼叫之 OLE 物件的方法名稱。  
  
 _returnvalue_  **輸出**  
 這是 OLE 物件的方法傳回值。 如果指定的話，它必須是適當資料類型的本機變數。  
  
 如果方法傳回單一值，請指定 *returnvalue*的本機變數，這會在本機變數中傳回方法傳回值，或不指定 *returnvalue*，這會將方法傳回值以單一資料行、單一資料列結果集的形式傳回給用戶端。  
  
 如果方法傳回值是 OLE 物件，則 *returnvalue* 必須是 **int**資料類型的本機變數。物件標記會儲存在本機變數中，而這個物件標記可以與其他 OLE Automation 預存程式一起使用。  
  
 當方法傳回值是陣列時，如果指定 *returnvalue* ，則會設定為 Null。  
  
 當發生下列中的任何狀況時，都會產生錯誤：  
  
-   *returnvalue* 已指定，但方法不會傳回值。  
  
-   方法傳回含有超出二維的陣列。  
  
-   方法在輸出參數中傳回陣列。  
  
`[ _@parametername = ] parameter[ OUTPUT ]` 是方法參數。 如果有指定， *參數* 必須是適當資料類型的值。  
  
 若要取得輸出參數的傳回值， *參數* 必須是適當資料類型的本機變數，且必須指定 **輸出** 。 如果指定了常數參數，或是未指定 **output** ，則會忽略來自輸出參數的任何傳回值。  
  
 如果有指定， *parametername* 必須是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 具名引數的名稱。 請注意， **@** _parametername_is 不是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 本機變數。 會移除 at sign (**@**) ，並將 *parametername*傳遞至 OLE 物件做為參數名稱。 您必須在指定好所有位置性參數之後，指定所有具名參數。  
  
 *n*  
 這是一個預留位置，表示可以指定多個參數。  
  
> [!NOTE]
>  * \@ parametername*可以是具名引數，因為它是指定方法的一部分，並且會傳遞至物件。 這個預存程序的其他參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊， [OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>結果集  
 如果方法傳回值是含有一或兩個維度的陣列，就會將陣列傳回用戶端作為結果集：  
  
-   一維陣列會以單一資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。 換言之，這個陣列是以 (columns) 的方式傳回。  
  
-   二維陣列會以多資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。資料行數目等於陣列第一維的元素數目，資料列數目等於陣列第二維的元素數目。 換言之，這個陣列是以 (columns, rows) 的方式傳回。  
  
 當屬性傳回值或方法傳回值為數組時， **sp_OAGetProperty** 或 **sp_OAMethod** 會將結果集傳回給用戶端。 (方法輸出參數不能是陣列。)這些程序會掃描陣列中的所有資料值來判斷適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，以及結果集中每個資料行所用的資料長度。 對於特定資料行，這些程序會利用資料類型和長度來表示這個資料行中的所有資料值。  
  
 當資料行中的所有資料值都共用相同的資料類型時，整個資料行都會使用這個資料類型。 當資料行中的資料值是不同資料類型時，便會根據下表來選擇整個資料行的資料類型。  
  
||int|FLOAT|money|Datetime|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>備註  
 您也可以使用 **sp_OAMethod** 來取得屬性值。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或直接在此預存程式上執行許可權。 `Ole Automation Procedures` 必須 **啟用** 設定，才能使用任何與 OLE Automation 相關的系統程式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calling-a-method"></a>A. 呼叫方法  
 下列範例會呼叫 `Connect` 先前建立的 **SQLServer** 物件的方法。  
  
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
 下列範例 `HostName` 會取得先前建立之 **SQLServer** 物件) 的屬性 (，並將其儲存在區域變數中。  
  
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
 [OLE Automation 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
