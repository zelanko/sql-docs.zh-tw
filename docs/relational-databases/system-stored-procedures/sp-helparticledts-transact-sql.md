---
title: sp_helparticledts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 022a2c8df27afdd3a9766e447f4030cdede4af4f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813190"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用來取得當利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 來建立轉換訂閱時，所用正確自訂工作名稱的相關資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication =**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是發行集的發行項名稱。 *發行項*已**sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|在複製快照集資料之前發生的程式設計工作之工作名稱。 如果發生指令碼錯誤，應該繼續執行程式。|  
|**pre_script_task_name**|**sysname**|在複製快照集資料之前發生的程式設計工作之工作名稱。 發生錯誤時，中止執行程式。|  
|**transformation_task_name**|**sysname**|使用資料驅動查詢工作時的程式設計工作之工作名稱。|  
|**post_script_ignore_error_task_name**|**sysname**|在複製快照集資料之後發生的程式設計工作之工作名稱。 如果發生指令碼錯誤，應該繼續執行程式。|  
|**post_script_task_name**|**sysname**|在複製快照集資料之後發生的程式設計工作之工作名稱。 發生錯誤時，中止執行程式。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helparticledts**用於快照式複寫和異動複寫。  
  
 當在 Data Transformation Services (DTS) 程式中命名作業時，必須遵照複寫代理程式所需要的一些命名慣例。 如果是自訂工作，如執行 SQL 工作，名稱就是發行項名稱、前置詞和選擇性部分的串連字串。 當撰寫程式碼時，如果您不確定工作名稱應該是什麼，結果集會提供應該使用的工作名稱。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色並**db_owner**固定的資料庫角色可以執行**sp_helparticledts**。  
  
  
