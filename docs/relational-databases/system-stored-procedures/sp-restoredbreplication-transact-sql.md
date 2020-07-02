---
title: sp_restoredbreplication （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c8d83d2aad9227993df29774d3140376514319ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633941"
---
# <a name="sp_restoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  如果將資料庫還原到在其他情況下無法執行複寫處理的非原始伺服器、資料庫或系統，便移除複寫設定。 將複寫的資料庫還原到並非備份來源的伺服器或資料庫時，無法保留複寫設定。 在還原時，伺服器會直接呼叫**sp_restoredbreplication** ，以自動從還原的資料庫中移除複寫中繼資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>引數  
`[ @srv_orig = ] 'original_server_name'`  
 建立備份的伺服器名稱。 *original_server_name*是**sysname**，沒有預設值。  
  
`[ @db_orig = ] 'original_database_name'`  
 已備份資料庫的名稱。 *original_database_name*是**sysname**，沒有預設值。  
  
`[ @keep_replication = ] keep_replication`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @perform_upgrade = ] perform_upgrade`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_restoredbreplication**用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）或**dbcreator**固定伺服器角色的成員或**dbo**資料庫架構，才能夠執行**sp_restoredbreplication**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
