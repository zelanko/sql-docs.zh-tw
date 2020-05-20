---
title: sp_addmergepartition （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0af6f62a45dd519f8a63839ae1435815569b93be
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831775"
---
# <a name="sp_addmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  針對訂閱者端[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)或[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)的值所篩選的訂用帳戶，建立動態篩選的分割區。 這個預存程序執行於所發行之資料庫的發行者端，它用來手動產生資料分割。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要在其上建立資料分割的合併式發行集。 *發行*集是**sysname**，沒有預設值。 如果指定了*suser_sname* ， *hostname*的值必須是 Null。  
  
`[ @suser_sname = ] 'suser_sname'`這是在建立訂閱的資料分割時所使用的值，此資料是由訂閱者端的[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函數值所篩選。 *suser_sname*是**sysname**，沒有預設值。  
  
`[ @host_name = ] 'host_name'`這是在建立訂閱的資料分割時所使用的值，此資料是由訂閱者端的[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函數值所篩選。 *host_name*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergepartition**用於合併式複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addmergepartition**。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
