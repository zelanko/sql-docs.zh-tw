---
title: sp_restoredbreplication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ea73a77c47b4579cda2e97dcea77a8f6516157c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32996985"
---
# <a name="sprestoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果將資料庫還原到在其他情況下無法執行複寫處理的非原始伺服器、資料庫或系統，便移除複寫設定。 將複寫的資料庫還原到並非備份來源的伺服器或資料庫時，無法保留複寫設定。 在還原時，伺服器會呼叫**sp_restoredbreplication**直接來自動移除還原的資料庫中的複寫中繼資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@srv_orig =** ] **'***original_server_name***'**  
 建立備份的伺服器名稱。 *original_server_name*是**sysname**，沒有預設值。  
  
 [  **@db_orig =** ] **'***original_database_name***'**  
 已備份資料庫的名稱。 *original_database_name*是**sysname**，沒有預設值。  
  
 [  **@keep_replication =** ] *keep_replication*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@perform_upgrade=** ] *perform_upgrade*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_restoredbreplication**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**或**dbcreator**固定的伺服器角色或**dbo**資料庫結構描述可以執行**sp_restoredbreplication**.  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
