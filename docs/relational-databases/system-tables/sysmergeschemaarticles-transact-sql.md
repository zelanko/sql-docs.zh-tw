---
title: sysmergeschemaarticles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f362fd55cab4f0b741db5ecf53201b06b1c4243e
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101526"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  追蹤合併式複寫之僅限結構描述的發行項。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|合併式發行集中僅限結構描述的發行項之名稱。|  
|**type**|**tinyint**|指出僅限結構描述的發行項之類型，它可以是下列項目之一：<br /><br /> **0x20** = 預存程序僅限結構描述發行項。<br /><br /> **0x40** = 檢視僅限結構描述發行項或索引的檢視僅限結構描述發行項。|  
|**objid**|**int**|發行項基底物件的物件識別碼。 它可以是程序、檢視、索引檢視或使用者定義函數的物件識別碼。|  
|**artid&lt**|**uniqueidentifier**|發行項識別碼。|  
|**description**|**nvarchar(255)**|發行項的描述。|  
|**pre_creation_command**|**tinyint**|當在訂閱資料庫中建立發行項時，所採取的預設動作。<br /><br /> **0 =** 無-如果資料表已存在於訂閱者上，會採取任何動作。<br /><br /> **1** = drop-卸除資料表，然後再重新建立它。<br /><br /> **2** = 刪除-發出一項刪除根據子集篩選中的 WHERE 子句。<br /><br /> **3** = 截斷-與相同**2**，但是會刪除頁面而不是資料列。 不過，它不用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|發行集的唯一識別碼。|  
|**status**|**tinyint**|指出僅限結構描述的發行項之狀態，它可以是下列項目之一：<br /><br /> **1** = 未-發行的資料表執行下一次執行快照集代理程式的初始處理指令碼。<br /><br /> **2** = active-已執行發行資料表的初始處理指令碼。<br /><br /> **5** = New_inactive-加入。<br /><br /> **6** = New_active-加入。|  
|**creation_script**|**nvarchar(255)**|用來建立目標資料表的選擇性發行項結構描述預先建立指令碼的路徑和名稱。|  
|**schema_option**|**binary(8)**|給定僅限結構描述的發行項之結構描述產生選項的點陣圖，它可能是一或多個這些值的位元邏輯 OR 結果：<br /><br /> **0x00** = 停用快照集代理程式的指令碼，並使用所提供的 CreationScript。<br /><br /> **0x01** = 產生物件的建立 （CREATE TABLE、 CREATE PROCEDURE 等等）。<br /><br /> **0x10** = 產生對應的叢集索引。<br /><br /> **0x20** = convert 的使用者定義資料類型轉換成基底資料型別。<br /><br /> **0x40** = 產生對應的非叢集索引。<br /><br /> **0x80** = 包含宣告式參考完整性的主索引鍵。<br /><br /> **0x100** = 資料表發行項，複寫的使用者觸發程序，如果定義的話。<br /><br /> **0x200** = 複寫 foreign key 條件約束。 如果參考的資料表不是發行集的一部份，便不會複寫發行資料表的所有外部索引鍵條件約束。<br /><br /> **0x400** = 複寫 check 條件約束。<br /><br /> **0x800** = 複寫預設值。<br /><br /> **0x1000** = 複寫資料行層級定序。<br /><br /> **0x2000** = 擴充屬性的發行的項來源物件相關聯的複寫。<br /><br /> **0x4000** = 複寫唯一索引鍵，如果資料表發行項上定義。<br /><br /> **0x8000** = 主索引鍵和唯一索引鍵的資料表發行項作為使用 ALTER TABLE 陳述式條件約束的複寫。<br /><br /> 如需有關可能的值，如**schema_option**，請參閱[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|訂閱資料庫中的目的地物件名稱。 這個值只適用於僅限結構描述的發行項，如預存程序、檢視和 UDF。|  
|**destination_owner**|**sysname**|在訂閱資料庫中，如果不是物件的擁有者**dbo**。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
