---
title: sp_OAGetProperty （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6efc0b620dcec300b5342ea5a0f63358fcdfadc5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68107884"
---
# <a name="sp_oagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  取得 OLE 物件的屬性值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>引數  
 *objecttoken*  
 這是先前使用**sp_OACreate**所建立之 OLE 物件的物件 token。  
  
 *propertyname*  
 這是要傳回之 OLE 物件的屬性名稱。  
  
 *propertyvalue* **輸出**  
 這是傳回的屬性值。 如果指定的話，它必須是適當資料類型的本機變數。  
  
 如果屬性傳回 OLE 物件， *propertyvalue*必須是**int**資料類型的本機變數。物件 token 會儲存在本機變數中，而且這個物件 token 可以與其他 OLE Automation 預存程式搭配使用。  
  
 如果屬性傳回單一值，請指定*propertyvalue*的本機變數，這會在本機變數中傳回屬性值;或不指定*propertyvalue*，這會將屬性值以單一資料行、單一資料列結果集的形式傳回用戶端。  
  
 當屬性傳回陣列時，如果指定了*propertyvalue* ，則會設定為 Null。  
  
 如果指定了*propertyvalue* ，但屬性並未傳回值，則會發生錯誤。 如果屬性傳回含有多於二個維度的陣列，就會發生錯誤。  
  
 *指數*  
 這是一個索引參數。 如果指定， *index*必須是適當資料類型的值。  
  
 部份屬性有參數。 這些屬性稱為索引屬性，參數稱為索引參數。 一個屬性可以有多個索引參數。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱[OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>結果集  
 如果屬性傳回含有一或兩個維度的陣列，就會將陣列傳回用戶端作為結果集：  
  
-   一維陣列會以單一資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。 換言之，會將陣列傳回作為資料行。  
  
-   二維陣列會以多資料列結果集的方式傳回給用戶端，這個資料列中有多個資料行，資料行數目等於陣列的元素數目。資料行數目等於陣列第一維的元素數目，資料列數目等於陣列第二維的元素數目。 換言之，這個陣列是以 (columns, rows) 的方式傳回。  
  
 當屬性傳回值或方法傳回值為數組時， **sp_OAGetProperty**或**sp_OAMethod**會將結果集傳回給用戶端。 (方法輸出參數不能是陣列。)這些程序會掃描陣列中的所有資料值來判斷適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，以及結果集中每個資料行所用的資料長度。 對於特定資料行，這些程序會利用資料類型和長度來表示這個資料行中的所有資料值。  
  
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
 您也可以使用**sp_OAMethod**來取得屬性值。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色的成員資格，或直接在這個預存程式上執行許可權。 `Ole Automation Procedures`必須**啟用**設定，才能使用與 OLE Automation 相關的任何系統程式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-local-variable"></a>A. 使用本機變數  
 下列範例會取得`HostName`屬性（先前建立的**SQLServer**物件），並將它儲存在本機變數中。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. 使用結果集  
 下列範例會取得`HostName`屬性（先前建立的**SQLServer**物件），並將它以結果集的形式傳回給用戶端。  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
