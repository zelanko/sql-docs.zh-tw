---
title: sp_helpmergedeleteconflictrows (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
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
- sp_helpmergedeleteconflictrows
- sp_helpmergedeleteconflictrows_TSQL
helpviewer_keywords:
- sp_helpmergedeleteconflictrows
ms.assetid: 222be651-5690-4341-9dfb-f9ec1d80c970
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f7d2fc014ae372b07417d88513f964a6d7f4795f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpmergedeleteconflictrows-transact-sql"></a>sp_helpmergedeleteconflictrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回遺失刪除衝突之資料列的相關資訊。 這個預存程序是在使用非集中式衝突記錄時，執行於發行集資料庫的發行者端，或訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergedeleteconflictrows [ [ @publication = ] 'publication']  
    [ , [ @source_object = ] 'source_object']  
    [ , [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publsher_db'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是**%**。 如果指定發行集的話，就會傳回發行集所限定的所有衝突。  
  
 [  **@source_object=**] **'***source_object***'**  
 這是來源物件的名稱。 *source_object*是**nvarchar （386)**，預設值是 NULL。  
  
 [ **@publisher=**] **'***publisher***'**  
 是發行者的名稱。*發行者*是**sysname**，預設值是 NULL。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。*publisher_db*是**sysname**，預設值是 NULL。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**source_object**|**nvarchar(386)**|刪除衝突的來源物件。|  
|**rowguid**|**uniqueidentifier**|刪除衝突的資料列識別碼。|  
|**conflict_type**|**int**|表示衝突類型的代碼：<br /><br /> **1** = UpdateConflict： 在資料列層級偵測到衝突。<br /><br /> **2** = ColumnUpdateConflict： 在資料行層級偵測到衝突。<br /><br /> **3** = UpdateDeleteWinsConflict： 刪除在衝突中獲勝。<br /><br /> **4** = UpdateWinsDeleteConflict： 衝突失敗且已刪除的 rowguid 會記錄在此資料表。<br /><br /> **5** = UploadInsertFailed： 訂閱者的插入無法套用在發行者端。<br /><br /> **6** = DownloadInsertFailed： 發行者的插入無法套用在訂閱者。<br /><br /> **7** = UploadDeleteFailed： 訂閱者 」 端的刪除無法上傳到 「 發行者 」。<br /><br /> **8** = DownloadDeleteFailed： 發行者的刪除無法下載到訂閱者。<br /><br /> **9** = UploadUpdateFailed： 訂閱者 」 端的更新無法套用在發行者端。<br /><br /> **10** = DownloadUpdateFailed： 發行者的更新無法套用到訂閱者。|  
|**reason_code**|**整數**|可為內容相關的錯誤碼。|  
|**reason_text**|**varchar(720)**|可為內容相關的錯誤描述。|  
|**origin_datasource**|**varchar(255)**|衝突的來源。|  
|**pubid**|**uniqueidentifier**|發行集識別碼。|  
|**MSrepl_create_time**|**datetime**|加入衝突資訊的時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergedeleteconflictrows**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色和**db_owner**固定的資料庫角色可以執行**sp_helpmergedeleteconflictrows**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
