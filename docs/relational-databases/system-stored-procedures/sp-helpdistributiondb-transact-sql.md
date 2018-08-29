---
title: sp_helpdistributiondb (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df4a44be4ef3271e6af8e7148bfee50f40c71617
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43018294"
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定散發資料庫的屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@database=**] **'***database_name***'**  
 這是要傳回屬性的資料庫名稱。 *database_name*已**sysname**，預設值是**%** 與散發者，並在其上相關聯的所有資料庫的使用者具有權限。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|散發資料庫的名稱。|  
|**min_distretention**|**int**|在刪除交易之前的最小保留期限 (以小時為單位)。|  
|**max_distretention**|**int**|在刪除交易之前的最大保留期限 (以小時為單位)。|  
|**記錄保留**|**int**|保留記錄的時數。|  
|**history_cleanup_agent**|**sysname**|記錄清除代理程式的名稱。|  
|**distribution_cleanup_agent**|**sysname**|散發清除代理程式的名稱。|  
|**status**|**int**|僅供內部使用。|  
|**data_folder**|**nvarchar(255)**|用來儲存資料庫檔案的目錄名稱。|  
|**data_file**|**nvarchar(255)**|資料庫檔案的名稱。|  
|**data_file_size**|**int**|初始資料檔大小 (以 MB 為單位)。|  
|**log_folder**|**nvarchar(255)**|資料庫記錄檔的目錄名稱。|  
|**log_file**|**nvarchar(255)**|記錄檔的名稱。|  
|**log_file_size**|**int**|初始記錄檔大小 (以 MB 為單位)。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdistributiondb**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 成員**db_owner**固定的資料庫角色或**replmonitor**散發資料庫中的角色及使用散發資料庫的發行集的發行集存取清單中的使用者可以執行**sp_helpdistributiondb**傳回檔案的相關資訊。 成員**公開金鑰**角色可以執行**sp_helpdistributiondb**傳回他們具有存取權的散發資料庫的非檔案相關資訊。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
