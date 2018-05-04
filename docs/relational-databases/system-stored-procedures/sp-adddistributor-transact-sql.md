---
title: sp_adddistributor (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 49b2250ac8c6a6ec634c1e141c28cc5056a80a24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一個項目中的[sys.sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md)資料表 （如果沒有的話），將標示為散發者，伺服器項目，再儲存屬性資訊。 這個預存程序執行於 master 資料庫的散發者端，以便登錄伺服器，並將伺服器標示為散發者。 如果是遠端散發者，它也會在 master 資料庫的發行者端執行，以登錄遠端散發者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@distributor=**] **'***散發者***'**  
 這是散發伺服器名稱。 *散發者*是**sysname**，沒有預設值。 只有在設定遠端散發者時，才使用這個參數。 它會新增為散發者屬性中的項目**msdb 資料庫...MSdistributor**資料表。  
  
 [  **@heartbeat_interval=**] *heartbeat_interval*  
 這是在未記錄進度訊息的情況下，代理程式所能執行的最大分鐘數。 *heartbeat_interval*是**int**，預設值是 10 分鐘。 系統會建立一項 SQL Server Agent 作業，依這個間隔來執行，以便檢查執行中之複寫代理程式的狀態。  
  
 [  **@password=**] **'***密碼***'**]  
 是的密碼**distributor_admin**登入。 *密碼*是**sysname**，預設值是 NULL。 如果是 NULL 或空字串，就會將密碼重設為隨機值。 當加入第一個遠端散發者時，必須設定密碼。 **distributor_admin**登入和*密碼*針對連結的伺服器項目，用於儲存*散發者*RPC 連線，包括本機連接。 如果*散發者*是本機電腦，密碼**distributor_admin**設為新值。 利用遠端散發者的發行者，相同的值為*密碼*執行時，必須指定**sp_adddistributor**發行者和散發者端。 [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)可以用來變更散發者密碼。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@from_scripting=** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddistributor**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_adddistributor**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
