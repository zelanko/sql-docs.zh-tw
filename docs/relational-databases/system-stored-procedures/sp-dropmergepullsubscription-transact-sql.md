---
title: sp_dropmergepullsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab2cda06971e56a8c15e2fb7382977a36fe7a34a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933880"
---
# <a name="sp_dropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除合併提取訂閱。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，預設值是 Null。 此為必要參數。 指定 [**全部**] 的值，以移除所有發行集的訂閱  
  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，預設值是 Null。 此為必要參數。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 Null。 此為必要參數。  
  
`[ @reserved = ] 'reserved'`保留供日後使用。 *reserved*是**bit**，預設值是**0**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergepullsubscription**用於合併式複寫中。  
  
 **sp_dropmergepullsubscription**會卸載這個合併提取訂閱的合併代理程式，但不會在**sp_addmergepullsubscription**中建立合併代理程式。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員或建立合併提取訂閱的使用者，才能夠執行**sp_dropmergepullsubscription**。 只有在建立合併提取訂閱的使用者屬於此角色時， **db_owner**固定資料庫角色才能夠執行**sp_dropmergepullsubscription** 。  
  
## <a name="see-also"></a>另請參閱  
 [刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
