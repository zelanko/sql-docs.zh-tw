---
title: MSmerge_conflicts_info （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflicts_info_TSQL
- MSmerge_conflicts_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflicts_info system table
ms.assetid: 6b76ae96-737a-4000-a6b6-fcc8772c2af4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7629bff37fb33080f8057fc1799437fff182882f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68044800"
---
# <a name="msmerge_conflicts_info-transact-sql"></a>MSmerge_conflicts_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflicts_info**資料表會追蹤同步處理合併式發行集的訂閱時所發生的衝突。 衝突的遺失資料列資料會儲存在發生衝突之發行項的[MSmerge_conflict_publication_article](../../relational-databases/system-tables/msmerge-conflict-publication-article-transact-sql.md)資料表中。 這份資料表儲存在發行集資料庫的發行者端，以及訂閱資料庫的訂閱者端。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已發行資料表的暱稱。|  
|**rowguid**|**uniqueidentifier**|衝突資料列的識別碼。|  
|**origin_datasource**|**nvarchar(255)**|引發衝突變更的資料庫名稱。|  
|**conflict_type**|**int**|發生衝突的類型，它可以是下列項目之一：<br /><br /> **1** = 更新衝突：在資料列層級偵測到衝突。<br /><br /> **2** = 資料行更新衝突：在資料行層級偵測到衝突。<br /><br /> **3** = 更新刪除 wins 衝突：刪除在衝突中獲勝。<br /><br /> **4** = 更新 Wins 刪除衝突：遺失衝突的已刪除 rowguid 會記錄在此資料表中。<br /><br /> **5** = 上傳插入失敗：訂閱者的插入無法套用於發行者端。<br /><br /> **6** = 下載插入失敗：無法在訂閱者端套用從發行者進行的插入。<br /><br /> **7** = 上傳刪除失敗：訂閱者端的刪除無法上傳到發行者。<br /><br /> **8** = 下載刪除失敗：「發行者」端的刪除無法下載到「訂閱者」。<br /><br /> **9** = 上傳更新失敗：訂閱者端的更新無法套用於發行者端。<br /><br /> **10** = 下載更新失敗：「發行者」端的更新無法套用至「訂閱者」。<br /><br /> **11** = 解析<br /><br /> **12** = 邏輯記錄更新 Wins 刪除：此資料表會記錄遺失衝突的已刪除邏輯記錄。<br /><br /> **13** = 邏輯記錄衝突插入更新：插入邏輯記錄與更新發生衝突。<br /><br /> **14** = 邏輯記錄刪除 Wins 更新衝突：失去衝突的已更新邏輯記錄會記錄在此資料表中。|  
|**reason_code**|**int**|可為內容相關的錯誤碼。 在更新-更新和更新-刪除衝突的情況下，用於此資料行的值與**conflict_type**相同。 但是，對於無法變更衝突，原因代碼將為錯誤，以防止「合併代理程式」套用變更。 例如，如果合併代理程式因為主鍵違規而無法在訂閱者端套用插入，它會記錄6的**conflict_type** （「下載插入失敗」）和**reason_code** 2627，這是主鍵違規的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內部錯誤訊息：「違反% ls 條件約束 '%. * ls '。 無法在物件 '% 中插入重複的索引鍵。\*ls '. "|  
|**reason_text**|**Nvarchar （720）**|可為內容相關的錯誤描述。|  
|**pubid**|**uniqueidentifier**|發行集的識別碼。|  
|**MSrepl_create_time**|**datetime**|發生衝突的時間。|  
|**origin_datasource_id**|**uniqueidentifier**|引發衝突變更的資料庫識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
