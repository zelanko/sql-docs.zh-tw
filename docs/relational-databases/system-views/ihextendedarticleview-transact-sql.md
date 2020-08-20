---
description: IHextendedArticleView (Transact-SQL)
title: IHextendedArticleView (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a56d2e7b96464866f0216e1f93ef6eb3d1066df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463865"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHextendedArticleView** view 會公開非 SQL Server 發行集中的發行項相關資訊。 這個視圖會儲存在 **散發** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|發行者的唯一識別碼。|  
|**publication_id**|**int**|發行集的唯一識別碼。|  
|**文章**|**sysname**|發行項的名稱|  
|**destination_object**|**sysname**|在訂閱者端之已發行物件的名稱。|  
|**source_owner**|**sysname**|在發行者端之已發行物件的擁有者。|  
|**source_object**|**sysname**|在發行者端之已發行物件的名稱。|  
|**description**|**nvarchar(255)**|發行項的描述。|  
|**creation_script**|**nvarchar(255)**|建立發行項之結構描述的指令碼。|  
|**del_cmd**|**nvarchar(255)**|針對 DELETE 來執行的命令。|  
|**濾波器**|**int**|用來定義水平資料分割之預存程序的識別碼。|  
|**filter_clause**|**ntext**|用來水平篩選發行項的 WHERE 子句。|  
|**ins_cmd**|**nvarchar(255)**|針對 INSERT 來執行的命令。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的前置建立命令：<br /><br /> **0** = 無。<br /><br /> **1** = 卸載。<br /><br /> **2** = 刪除。<br /><br /> **3** = 截斷。|  
|**status**|**tinyint**|發行項選項和狀態的位元遮罩，它可能是一或多個這些值的位元邏輯 OR 結果：<br /><br /> **1** = 發行項為使用中。<br /><br /> **8** = 在 INSERT 語句中包含資料行名稱。<br /><br /> **16** = 使用參數化語句。<br /><br /> **24** = 兩者都會在 INSERT 語句中包含資料行名稱，並使用參數化語句。<br /><br /> 例如，使用參數化語句的使用中發行項在此資料行中的值為 **17** 。 **0**值表示發行項為非使用中，且未定義任何其他屬性。|  
|**type**|**tinyint**|發行項類型：<br /><br /> **1** = 記錄式發行項。<br /><br /> **3** = 具有手動篩選的記錄式發行項。<br /><br /> **5** = 具有手動 view 的記錄式文章。<br /><br /> **7** = 具有手動篩選和手動視圖的記錄式發行項。|  
|**upd_cmd**|**nvarchar(255)**|針對 UPDATE 來執行的命令。|  
|**schema_option**|**binary**|指出要編寫腳本的內容。如需支援的架構選項清單，請參閱 [sp_addarticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 。|  
|**dest_owner**|**sysname**|目的地資料庫已發行之物件的擁有者。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
