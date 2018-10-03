---
title: sysschemaarticles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sysschemaarticles_TSQL
- sysschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysschemaarticles system table
ms.assetid: 67a1c039-c283-4a9c-bacc-b9b3973590c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37d064411927a112a50e9ff64a9e8a6dedefb3e5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765406"
---
# <a name="sysschemaarticles-transact-sql"></a>sysschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  追蹤交易式和快照式發行集之僅限結構描述的發行項。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**artid&lt**|**int**|發行項識別碼。|  
|**creation_script**|**nvarchar(255)**|用來建立目標資料表的發行項結構描述指令碼之路徑和名稱。|  
|**description**|**nvarchar(255)**|發行項的描述性項目。|  
|**dest_object**|**sysname**|如果發行項是僅限結構描述的發行項，如預存程序、檢視或 UDF，便是訂閱資料庫中之物件的名稱。|  
|**name**|**sysname**|發行集中僅限結構描述的發行項之名稱。|  
|**objid**|**int**|發行項基底物件的物件識別碼。 它可以是程序、檢視、索引檢視或 UDF 的物件識別碼。|  
|**pubid**|**int**|發行集的識別碼。|  
|**pre_creation_cmd**|**tinyint**|指定如果在套用這個發行項的快照集時，在訂閱者端偵測到現有的同名物件，系統應該採取的動作：<br /><br /> **0** = nothing。<br /><br /> **1** = 刪除目的地資料表。<br /><br /> **2** = 卸除目的地資料表。<br /><br /> **3** = 截斷目的地資料表。|  
|**status**|**int**|用來表示發行項狀態的點陣圖。|  
|**type**|**tinyint**|指示僅限結構描述的發行項之值：<br /><br /> **32** = 預存程序。<br /><br /> **64** = 檢視或索引檢視表。 <br /><br /> **96** = 彙總函式。<br /><br /> **128** = 函式。|  
|**schema_option**|**binary(8)**|給定發行項之結構描述產生選項的位元遮罩。 它指定在目的地資料庫中，針對所有 CALL/MCALL/XCALL 語法來自動建立預存程序，它可能是一或多個這些值的位元邏輯 OR 結果：<br /><br /> **0x00** = 停用快照集代理程式，並使用指令碼*creation_script*。<br /><br /> **0x01** = 產生物件的建立 （CREATE TABLE、 CREATE PROCEDURE 等等）。 這個值是預存程序發行項的預設值。<br /><br /> **0x02** = 產生自訂預存程序發行項，如果定義的話。<br /><br /> **0x10** = 產生對應的叢集索引。<br /><br /> **0x20** = 將使用者定義資料類型轉換成基底資料型別。<br /><br /> **0x40**= 產生對應的非叢集索引。<br /><br /> **0x80**= 包括主索引鍵中宣告式參考完整性。<br /><br /> **0x73** = 產生 CREATE TABLE 陳述式、 建立叢集和非叢集索引，將轉換成基底資料類型的使用者定義資料類型並產生自訂預存程序可套用在訂閱者的指令碼。 這個值是預存程序發行項以外之所有發行項的預設值。<br /><br /> **0x100**= 複寫資料表發行項上的使用者觸發程序，如果定義的話。<br /><br /> **0x200**= 複寫 foreign key 條件約束。 如果參考的資料表不是發行集的一部份，便不會複寫所發行之資料表的所有外部索引鍵條件約束。<br /><br /> **0x400**= 複寫 check 條件約束。<br /><br /> **0x800**= 複寫預設值。<br /><br /> **0x1000**= 複寫資料行層級定序。<br /><br /> **0x2000**= 擴充屬性的發行的項來源物件相關聯的複寫。<br /><br /> **0x4000**= 複寫唯一索引鍵，如果資料表發行項上定義。<br /><br /> **0x8000**= 複寫主索引鍵和唯一索引鍵的資料表發行項，作為使用 ALTER TABLE 陳述式條件約束。|  
|**dest_owner**|**sysname**|目的地資料庫的資料表擁有者。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
