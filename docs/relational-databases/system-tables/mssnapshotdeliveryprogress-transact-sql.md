---
title: MSsnapshotdeliveryprogress （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: stevestein
ms.author: sstein
ms.openlocfilehash: 638bea3db68712300ad2284e50676bf1df67c9ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139805"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  當套用快照集時，會使用**MSsnapshotdeliveryprogress**資料表來追蹤已成功傳遞至訂閱者的檔案。 這項資料用來繼續傳遞檔案，萬一合併代理程式在工作階段無法傳遞所有的檔案，那麼下次再執行合併代理程式時，不會再重複傳遞相同的檔案。 這份資料表儲存在訂閱資料庫的訂閱者端。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|識別通往順利傳遞檔案之快照集資料夾的路徑。 針對使用參數化篩選的發行集，字串**dynsnap**會附加至值。|  
|**progress_token_hash**|**int**|根據*progress_token*值所產生的雜湊值，可用來改善給定*progress_token*值的查閱效率。|  
|**progress_token**|**Nvarchar （500）**|識別已經順利傳遞的檔案，該值是檔案名稱和路徑的組合。|  
|**progress_timestamp**|**datetime**|表示快照集檔案成功傳遞的**日期時間**值。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
