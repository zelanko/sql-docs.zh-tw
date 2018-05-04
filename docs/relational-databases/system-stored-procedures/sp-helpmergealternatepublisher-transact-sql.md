---
title: sp_helpmergealternatepublisher (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords:
- sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9a66e9c0343a4441d3a5bf370d96ff7f6bf61370
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回啟用為合併式發行集的替代發行者之所有伺服器的清單。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是替代發行者的名稱。*發行者*是**sysname**，沒有預設值。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行集資料庫的名稱。*publisher_db*是**sysname**，沒有預設值。  
  
 [ **@publication=**] **'***publication***'**  
 是發行集名稱。*發行集*是**sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|替代發行者的名稱。|  
|**alternate_publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**alternate_publication**|**sysname**|發行集的名稱。|  
|**alternate_distributor**|**sysname**|散發者的名稱。|  
|**friendly_name**|**nvarchar(255)**|替代發行者的描述。|  
|**enabled**|**bit**|指定伺服器是否為替代發行者。 **1**指定發行者啟用為替代發行者。 **0**指定不啟用。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergealternatepublisher**用於合併式複寫中。  
  
 在每個合併工作階段期間，系統會查詢發行者和訂閱者來分別找出它們的替代發行者清單。 合併處理序會加入或卸除替代發行者清單中的項目，結果是在訂閱者端和發行者端都相符的替代發行者清單。  
  
## <a name="permissions"></a>Permissions  
 只有發行集之發行集存取清單成員可以執行**sp_helpmergealternatepublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
