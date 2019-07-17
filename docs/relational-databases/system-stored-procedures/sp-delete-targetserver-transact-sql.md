---
title: sp_delete_targetserver 來 (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 487d88a7580432bf947893920d307e2f0adffd18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111996"
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
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
`[ @server_name = ] 'server'` 要移除為可用的目標伺服器的伺服器名稱。 *伺服器*已**nvarchar(30)** ，沒有預設值。  
  
`[ @clear_downloadlist = ] clear_downloadlist` 指定是否要清除目標伺服器的下載清單。 *clear_downloadlist*是型別**位元**，預設值是**1**。 當*clear_downloadlist*是**1**，程序刪除伺服器之前，清除伺服器的下載清單。 當*clear_downloadlist*是**0**，則不會清除下載清單。  
  
`[ @post_defection = ] post_defection` 指定是否要將脫離指示公佈在目標伺服器。 *post_defection&lt*是型別**元**，預設值是 1。 當*post_defection&lt*是**1**，程序將脫離指示公佈至目標伺服器之前先刪除伺服器。 當*post_defection&lt*是**0**，程序不會不脫離指示公佈至目標伺服器。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 刪除目標伺服器的一般方法是呼叫**sp_msx_defect**在目標伺服器。 使用**sp_delete_targetserver 來**手動脫離時才需要。  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須授與**sysadmin**固定的伺服器角色。  
  
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
 [sp_help_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
