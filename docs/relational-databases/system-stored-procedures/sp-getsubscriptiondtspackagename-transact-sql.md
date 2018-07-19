---
title: sp_getsubscriptiondtspackagename (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- sp_getsubscriptiondtspackagename
- sp_getsubscriptiondtspackagename_TSQL
helpviewer_keywords:
- sp_getsubscriptiondtspackagename
ms.assetid: 606c40aa-2593-43af-9762-0f260bbb51f2
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 755cd58c1e67ad0136e030cc63ae5d03437b76da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994265"
---
# <a name="spgetsubscriptiondtspackagename-transact-sql"></a>sp_getsubscriptiondtspackagename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回在資料傳送給訂閱者之前，用來轉換資料的 Data Transformation Services (DTS) 封裝名稱。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_getsubscriptiondtspackagename [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication**=] **'***發行集***'**  
 這是發行集的名稱。 **'***發行集***'** 是**sysname**，沒有預設值。  
  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是 sysname，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**new_package_name**|**sysname**|DTS 封裝的名稱。|  
  
## <a name="remarks"></a>備註  
 **sp_getsubscriptiondtspackagename**用於快照式複寫和異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_getsubscriptiondtspackagename**。  
  
  
