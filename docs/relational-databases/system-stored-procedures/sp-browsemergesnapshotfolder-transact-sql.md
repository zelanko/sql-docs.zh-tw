---
title: sp_browsemergesnapshotfolder (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsemergesnapshotfolder
- sp_browsemergesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsemergesnapshotfolder
ms.assetid: e248642f-5fea-4ed7-be1a-36ff75abcfde
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 378d7dc0a02d356cf505bb37007d7aa6b4033df8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818780"
---
# <a name="spbrowsemergesnapshotfolder-transact-sql"></a>sp_browsemergesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回針對合併式發行集而產生之最新快照集的完整路徑。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_browsemergesnapshotfolder [@publication= ] 'publication'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(2000)**|快照集目錄的完整路徑。|  
  
## <a name="remarks"></a>備註  
 **sp_browsemergesnapshotfolder**用於合併式複寫中。  
  
 如果將發行集設定成同時在發行者工作目錄和發行者快照集資料夾中產生快照集檔案，結果集會包含兩個資料列。第一個資料列包含發行集快照集資料夾，第二個資料列包含發行者工作目錄。  
  
 **sp_browsemergesnapshotfolder**判斷產生合併快照集檔案的目錄時很有用。 之後，就可以從替代快照集位置中，將這個資料夾/路徑及其內容複製到抽取式媒體，以及用來同步處理訂閱的快照集。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_browsemergesnapshotfolder**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
