---
title: sp_dropmergealternatepublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1a74cc2e0a91b33fc5fef6abf1202231927be25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689242"
---
# <a name="spdropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從合併式發行集中移除替代的發行者。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是目前發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是目前發行集資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [  **@publication =**] **'***發行集***'**  
 這是目前發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@alternate_publisher=**] **'***alternate_publisher***'**  
 這是要做為替代同步處理夥伴來卸除的替代發行者名稱。 *alternate_publisher*已**sysname**，沒有預設值。  
  
 [  **@alternate_publisher_db=**] **'***alternate_publisher_db***'**  
 這是要做為替代同步處理夥伴發行集資料庫來卸除的發行集資料庫名稱。 *alternate_publisher_db*已**sysname**，沒有預設值。  
  
 [  **@alternate_publication=**] **'***alternate_publication***'**  
 這是要做為替代同步處理夥伴發行集來卸除的發行集名稱。 *alternate_publication*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergealternatepublisher**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropmergelternatepublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergealternatepublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
