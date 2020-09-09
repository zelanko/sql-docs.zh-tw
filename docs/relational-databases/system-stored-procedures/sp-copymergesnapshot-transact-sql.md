---
description: sp_copymergesnapshot (Transact-SQL)
title: sp_copymergesnapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copymergesnapshot
- sp_copymergesnapshot_TSQL
helpviewer_keywords:
- sp_copymergesnapshot
ms.assetid: eaecd6e0-8486-4e5d-ace7-8ae75768c0a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f763c28087802df2dd3922b54829f6dee888545
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536654"
---
# <a name="sp_copymergesnapshot-transact-sql"></a>sp_copymergesnapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  將指定之發行集的快照集資料夾複製到** \@ destination_folder**中列出的資料夾。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要複製其快照集內容的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @destination_folder = ] 'destination_folder'` 這是要複製發行集快照集內容的資料夾名稱。 *destination_folder*是 **Nvarchar (255) **，沒有預設值。 *Destination_folder*可以是替代位置，例如在另一部伺服器、網路磁碟機機或卸載式媒體上 (例如 cd-rom 或抽取式磁碟) 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_copymergesnapshot** 用於合併式複寫中。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行7.0 版及更早版本的訂閱者無法使用替代快照集位置。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_copymergesnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../../relational-databases/replication/snapshot-options.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
