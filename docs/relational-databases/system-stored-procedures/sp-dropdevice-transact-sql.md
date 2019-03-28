---
title: sp_dropdevice (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropdevice_TSQL
- sp_dropdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], deleting
- sp_dropdevice
ms.assetid: c8b07189-7c35-414b-acc1-45bd6e7e17c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 633dff3e79a32f73c9ec7c4c376a60969db45aef
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531770"
---
# <a name="spdropdevice-transact-sql"></a>sp_dropdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從執行個體中卸除資料庫裝置或備份裝置[!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)]，刪除的項目**master.dbo.sysdevices**。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @logicalname = ] 'device'` 是資料庫裝置或備份裝置的邏輯名稱，如下所示**master.dbo.sysdevices.name**。 *裝置*已**sysname**，沒有預設值。  
  
`[ @delfile = ] 'delfile'` 指定是否應該刪除實體備份裝置檔。 *delfile*已**varchar(7)**。 如果指定為**DELFILE**，刪除實體備份裝置磁碟檔。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_dropdevice**無法在交易內部使用。  
  
## <a name="permissions"></a>Permissions  
 需要 **diskadmin** 固定伺服器角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中卸除 `tapedump1` 磁帶傾印裝置。  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [刪除備份裝置&#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
