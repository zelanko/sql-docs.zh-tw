---
title: sysschemaarticles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 89a9c9e8034fecad29cdd1f1c6c469e40c613436
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881287"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  追蹤交易式和快照式發行集之僅限結構描述的發行項。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|發行項識別碼。|  
|**creation_script**|**nvarchar(255)**|用來建立目標資料表的發行項結構描述指令碼之路徑和名稱。|  
|**description**|**nvarchar(255)**|發行項的描述性項目。|  
|**dest_object**|**sysname**|如果發行項是僅限結構描述的發行項，如預存程序、檢視或 UDF，便是訂閱資料庫中之物件的名稱。|  
|**name**|**sysname**|發行集中僅限結構描述的發行項之名稱。|  
|**objid**|**int**|發行項基底物件的物件識別碼。 它可以是程序、檢視、索引檢視或 UDF 的物件識別碼。|  
|**pubid**|**int**|發行集的識別碼。|  
|**pre_creation_cmd**|**tinyint**|指定如果在套用這個發行項的快照集時，在訂閱者端偵測到現有的同名物件，系統應該採取的動作：<br /><br /> **0** = 無任何內容。<br /><br /> **1** = 刪除目的地資料表。<br /><br /> **2** = 卸載目的地資料表。<br /><br /> **3** = 截斷目的地資料表。|  
|**status**|**int**|用來表示發行項狀態的點陣圖。|  
|**type**|**tinyint**|指示僅限結構描述的發行項之值：<br /><br /> **32** = 預存程式。<br /><br /> **64** = view 或 indexed view。 <br /><br /> **96** = 彙總函式。<br /><br /> **128** = 函數。|  
|**schema_option**|**binary （8）**|給定發行項之結構描述產生選項的位元遮罩。 它指定在目的地資料庫中，針對所有 CALL/MCALL/XCALL 語法來自動建立預存程序，它可能是一或多個這些值的位元邏輯 OR 結果：<br /><br /> **0x00** = 停用快照集代理程式的腳本，並使用*creation_script*。<br /><br /> **0x01** = 產生物件建立（CREATE TABLE、建立程式等等）。 這個值是預存程序發行項的預設值。<br /><br /> **0x02** = 產生發行項的自訂預存程式（如果有定義的話）。<br /><br /> **0x10** = 產生對應的叢集索引。<br /><br /> **0x20** = 將使用者自訂資料類型轉換成基底資料類型。<br /><br /> **0x40**= 產生對應的非叢集索引。<br /><br /> **0x80**= 包括主鍵的宣告參考完整性。<br /><br /> **0x73** = 產生 CREATE TABLE 語句、建立叢集和非叢集索引、將使用者定義資料類型轉換成基底資料類型，以及產生要在訂閱者端套用的自訂預存程式腳本。 這個值是預存程序發行項以外之所有發行項的預設值。<br /><br /> **0x100**= 複寫資料表發行項的使用者觸發程式（如果有定義的話）。<br /><br /> **0x200**= 複寫外鍵條件約束。 如果參考的資料表不是發行集的一部份，便不會複寫所發行之資料表的所有外部索引鍵條件約束。<br /><br /> **0x400**= 複製 check 條件約束。<br /><br /> **0x800**= 複寫預設值。<br /><br /> **0x1000**= 複寫資料行層級定序。<br /><br /> **0x2000**= 複寫與已發行之文章來源物件相關聯的擴充屬性。<br /><br /> **0x4000**= 如果在資料表發行項上定義了唯一索引鍵，則會進行複製。<br /><br /> **0x8000**= 複寫資料表發行項的主鍵和唯一索引鍵，做為使用 ALTER table 語句的條件約束。|  
|**dest_owner**|**sysname**|目的地資料庫的資料表擁有者。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
