---
title: sp_restoredbreplication & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e116b0350e23f3ae86e3c7de819b47ecae13baf
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534690"
---
# <a name="sprestoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果將資料庫還原到在其他情況下無法執行複寫處理的非原始伺服器、資料庫或系統，便移除複寫設定。 將複寫的資料庫還原到並非備份來源的伺服器或資料庫時，無法保留複寫設定。 在還原時，伺服器就會呼叫**sp_restoredbreplication**直接以自動移除還原的資料庫中的複寫中繼資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>引數  
`[ @srv_orig = ] 'original_server_name'` 備份建立所在的伺服器名稱。 *original_server_name&lt*已**sysname**，沒有預設值。  
  
`[ @db_orig = ] 'original_database_name'` 備份資料庫的名稱。 *original_database_name*已**sysname**，沒有預設值。  
  
`[ @keep_replication = ] keep_replication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @perform_upgrade = ] perform_upgrade` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_restoredbreplication**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**或是**dbcreator**固定的伺服器角色或**dbo**資料庫結構描述可以執行**sp_restoredbreplication**.  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
