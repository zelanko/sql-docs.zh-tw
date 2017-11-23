---
title: "sp_browsesnapshotfolder (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords: sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b31f3bb0e865452fd6f557a4832b04a21c11624
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回針對發行集而產生之最新快照集的完整路徑。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=**] **'***發行集***'**  
 這是發行項所在的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|快照集目錄的完整路徑。|  
  
## <a name="remarks"></a>備註  
 **sp_browsesnapshotfolder**用於快照式複寫和異動複寫。  
  
 如果*訂閱者*和*subscriber_db*欄位都保留 NULL，預存程序會傳回最新的快照集，它可以找到發行集的快照集資料夾。 如果*訂閱者*和*subscriber_db*指定欄位，預存程序會傳回指定之訂閱的快照集資料夾。 如果尚未產生發行集的快照集，就會傳回空結果集。  
  
 如果將發行集設定成同時在發行者工作目錄和發行者快照集資料夾中產生快照集檔案，結果集會包含兩個資料列。 第一個資料列包含發行集快照集資料夾，第二個資料列包含發行者工作目錄。 **sp_browsesnapshotfolder**判斷產生快照集檔案的目錄時很有用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_browsesnapshotfolder**。  
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
