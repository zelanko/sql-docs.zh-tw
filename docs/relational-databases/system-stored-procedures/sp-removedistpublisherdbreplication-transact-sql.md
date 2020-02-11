---
title: sp_removedistpublisherdbreplication （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 49c06ac45a91014199caa75c5893971f6f3de715
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771026"
---
# <a name="sp_removedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  移除屬於散發者特定發行集的發行中繼資料。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者伺服器的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname** ，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 異動複寫和快照式複寫會使用**sp_removedistpublisherdbreplication** 。  
  
 當必須同時卸載散發資料庫而重新建立已發行的資料庫時，就會使用**sp_removedistpublisherdbreplication** 。 下列中繼資料會被移除：  
  
-   所有的發行集中繼資料。  
  
-   所有屬於發行集之發行項的中繼資料。  
  
-   所有發行集訂閱的中繼資料。  
  
-   所有屬於發行集的複寫代理程式作業的中繼資料。  
  
## <a name="permissions"></a>權限  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色成員，或散發資料庫中之**db_owner**固定資料庫角色的成員，才能夠執行**sp_removedistpublisherdbreplication**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
