---
title: sp_addmergepartition & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd85b99afcbab5316f7a7dcc0cccd69eb7d5f0c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852226"
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立訂用帳戶篩選的值來動態篩選的資料分割[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)或是[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 「 訂閱者 」。 這個預存程序執行於所發行之資料庫的發行者端，它用來手動產生資料分割。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication**=] **'***發行集***'**  
 這是資料分割建立所在的合併式發行集。 *發行集*已**sysname**，沒有預設值。 如果*suser_sname*指定的值*hostname*必須是 NULL。  
  
 [ **@suser_sname**=] **'***suser_sname***'**  
 建立訂用帳戶的資料分割篩選的值時所用的值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函式，在訂閱者。 *suser_sname*已**sysname**，沒有預設值。  
  
 [ **@host_name**=] **'***host_name***'**  
 建立訂用帳戶的資料分割篩選的值時所用的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式，在訂閱者。 *host_name*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergepartition**用於合併式複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepartition**。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數化篩選的合併式發行集建立快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
