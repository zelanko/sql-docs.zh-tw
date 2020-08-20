---
description: sp_OASetProperty (Transact-SQL)
title: sp_OASetProperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OASetProperty
- sp_OASetProperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OASetProperty
ms.assetid: 0fe7d554-6b67-4d55-9d3e-4096802c47f8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b15d0c0e7d28973ef0803041b421c30517f0665
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473920"
---
# <a name="sp_oasetproperty-transact-sql"></a>sp_OASetProperty (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將 OLE 物件的屬性設為新值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_OASetProperty objecttoken , propertyname , newvalue [ , index... ]  
```  
  
## <a name="arguments"></a>引數  
 *objecttoken*  
 這是先前由 **sp_OACreate**所建立之 OLE 物件的物件 token。  
  
 *propertyname*  
 這是要設為新值的 OLE 物件屬性名稱。  
  
 *newvalue*  
 這是屬性的新值，必須是適當資料類型的值。  
  
 *指數*  
 這是一個索引參數。 如果有指定， *索引* 必須是適當資料類型的值。  
  
 部份屬性有參數。 這些屬性稱為索引屬性，參數稱為索引參數。 一個屬性可以有多個索引參數。  
  
> [!NOTE]  
>  這個預存程序的參數是依照位置來指定，而不是名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)，這個數字是 OLE Automation 物件所傳回之 HRESULT 的整數值。  
  
 如需 HRESULT 傳回碼的詳細資訊，請參閱 [OLE Automation 傳回碼和錯誤資訊](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或直接在此預存程式上執行許可權。 `Ole Automation Procedures` 必須 **啟用** 設定，才能使用任何與 OLE Automation 相關的系統程式。  
  
## <a name="examples"></a>範例  
 下列範例會將 `HostName` 先前建立的 **SQLServer** 物件的屬性 (設定為新值) 。  
  
```  
EXEC @hr = sp_OASetProperty @object, 'HostName', 'Gizmo';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END'  
```  
  
## <a name="see-also"></a>另請參閱  
 [OLE Automation 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE Automation 範例指令碼](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
