---
title: sp_removedistpublisherdbreplication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_removedistpublisherdbreplication_TSQL
- sp_removedistpublisherdbreplication
helpviewer_keywords:
- sp_removedistpublisherdbreplication
ms.assetid: 9bfe002a-25b5-4226-bcfb-feb2060d6b4a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 254794d97ab25a91bd583ffa9b1459469eed48ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769707"
---
# <a name="spremovedistpublisherdbreplication-transact-sql"></a>sp_removedistpublisherdbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除屬於散發者特定發行集的發行中繼資料。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_removedistpublisherdbreplication [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是發行者伺服器的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 這是發行集資料庫的名稱。 *publisher_db*已**sysname**沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_removedistpublisherdbreplication**交易式與快照式複寫所使用。  
  
 **sp_removedistpublisherdbreplication**必須重新建立已發行的資料庫，而不需要也卸除散發資料庫時，會使用。 下列中繼資料會被移除：  
  
-   所有的發行集中繼資料。  
  
-   所有屬於發行集之發行項的中繼資料。  
  
-   所有發行集訂閱的中繼資料。  
  
-   所有屬於發行集的複寫代理程式作業的中繼資料。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者端**db_owner**散發資料庫中的固定的資料庫角色可以執行**sp_removedistpublisherdbreplication**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
