---
title: sp_replmonitorhelppublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
ms.openlocfilehash: ba2c2a15efda0ca096d0f3d50acf60407b5dc86a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950553"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回散發者所關聯的一或多個發行者目前的狀態資訊。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是受監視的狀態 「 發行者 」 的名稱。 *發行者*已**sysname**，預設值是 NULL。 如果是 NULL，就會傳回所有使用散發者之發行者的資訊。  
  
`[ @refreshpolicy = ] refreshpolicy` 僅供內部使用。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|這是發行者的名稱。|  
|**distribution_db**|**sysname**|這是給定發行者所用之散發資料庫的名稱。|  
|**status**|**int**|這個發行者的發行集所有相關聯之複寫代理程式的最大值狀態，它可能是下列值之一。<br /><br /> **1** = 啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 正在重試<br /><br /> **6** = 失敗|  
|**警告**|**int**|屬於這個發行者的發行集之訂閱所產生的臨界值警告最大值，它可能是一個或多個這些值的邏輯 OR 結果。<br /><br /> **1** = 到期-交易式發行集的訂閱尚未同步保留期限臨界值內。<br /><br /> **2** = latency-將交易式發行者資料複寫到訂閱者所花的時間超出臨界值，以秒為單位。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱尚未同步保留期限臨界值內。<br /><br /> **8** = mergefastrunduration-完成合併訂閱的同步處理所花費的時間超出臨界值，以秒為單位，快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱的同步處理所花費的時間超出臨界值，以秒為單位，慢速或撥號網路連線。<br /><br /> **32** = mergefastrunspeed-傳遞速率無法維持臨界速率，以每秒的資料列快速網路連接合併訂閱同步處理期間，資料列。<br /><br /> **64** = mergeslowrunspeed-傳遞速率的合併訂閱同步處理期間，資料列無法維持臨界速率，以每秒的資料列，透過慢速或撥號網路連線。|  
|**publicationcount**|**int**|這是屬於發行者的發行集數目。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelppublisher**搭配所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者端**db_owner**或是**replmonitor**散發資料庫中的固定的資料庫角色可以執行**sp_replmonitorhelppublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
