---
title: sp_delete_targetserver （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0ccefc43c687c60d1dee030bf5f16a4b138224dd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833290"
---
# <a name="sp_delete_targetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從可用目標伺服器清單中，移除指定的伺服器。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>引數  
`[ @server_name = ] 'server'`要移除為可用目標伺服器的伺服器名稱。 *伺服器*是**Nvarchar （30）**，沒有預設值。  
  
`[ @clear_downloadlist = ] clear_downloadlist`指定是否要清除目標伺服器的下載清單。 *clear_downloadlist*是類型**bit**，預設值是**1**。 當*clear_downloadlist*為**1**時，此程式會先清除伺服器的下載清單，再刪除伺服器。 當*clear_downloadlist*為**0**時，不會清除下載清單。  
  
`[ @post_defection = ] post_defection`指定是否要將瑕疵指示張貼至目標伺服器。 *post_defection*是類型**bit**，預設值是1。 當*post_defection*為**1**時，此程式會在刪除伺服器之前，將瑕疵指示張貼到目標伺服器。 當*post_defection*為**0**時，此程式不會將缺失指示張貼至目標伺服器。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 刪除目標伺服器的一般方式是呼叫目標伺服器上的**sp_msx_defect** 。 只有在需要手動脫離時，才使用**sp_delete_targetserver** 。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須被授與**系統管理員（sysadmin** ）固定伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會從可用的作業伺服器群組中，移除 `LONDON1` 伺服器。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
