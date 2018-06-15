---
title: IHextendedArticleView (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2e0bcc294189f4902fd8d39de230166e6956dd53
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33010375"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedArticleView**檢視會公開非 SQL Server 發行集中發行項資訊。 這份檢視儲存在**發佈**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|發行者的唯一識別碼。|  
|**publication_id**|**int**|發行集的唯一識別碼。|  
|**article**|**sysname**|發行項的名稱|  
|**destination_object**|**sysname**|在訂閱者端之已發行物件的名稱。|  
|**source_owner**|**sysname**|在發行者端之已發行物件的擁有者。|  
|**source_object**|**sysname**|在發行者端之已發行物件的名稱。|  
|**描述**|**nvarchar(255)**|發行項的描述。|  
|**creation_script**|**nvarchar(255)**|建立發行項之結構描述的指令碼。|  
|**del_cmd**|**nvarchar(255)**|針對 DELETE 來執行的命令。|  
|**filter**|**int**|用來定義水平資料分割之預存程序的識別碼。|  
|**filter_clause**|**ntext**|用來水平篩選發行項的 WHERE 子句。|  
|**ins_cmd**|**nvarchar(255)**|針對 INSERT 來執行的命令。|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE、DELETE TABLE 或 TRUNCATE 的前置建立命令：<br /><br /> **0** = 無。<br /><br /> **1** = 卸除。<br /><br /> **2** = 刪除。<br /><br /> **3** = TRUNCATE。|  
|**status**|**tinyint**|發行項選項和狀態的位元遮罩，它可能是一個或多個這些值的位元邏輯 OR 結果：<br /><br /> **1** = 發行項在使用中。<br /><br /> **8** = 資料行名稱包括在 INSERT 陳述式。<br /><br /> **16** = 使用參數化陳述式。<br /><br /> **24** = 這包括在 INSERT 陳述式的資料行名稱，並使用參數化陳述式。<br /><br /> 例如，使用參數化陳述式的使用中發行項會有值為**17**這個資料行中。 值為**0**表示發行項不在非使用中，而且沒有其他的屬性定義。|  
|**type**|**tinyint**|發行項類型：<br /><br /> **1** = 記錄式發行項。<br /><br /> **3** = 含有手動篩選記錄檔為基礎的發行項。<br /><br /> **5** = 含有手動檢視的記錄式發行項。<br /><br /> **7** = 含有手動篩選和手動檢視的記錄式發行項。|  
|**upd_cmd**|**nvarchar(255)**|針對 UPDATE 來執行的命令。|  
|**schema_option**|**binary**|指出要編寫指令碼的項目。請參閱[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)如需支援的結構描述選項的清單。|  
|**dest_owner**|**sysname**|目的地資料庫已發行之物件的擁有者。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
