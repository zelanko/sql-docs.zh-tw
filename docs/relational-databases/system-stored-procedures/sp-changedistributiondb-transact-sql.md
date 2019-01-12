---
title: sp_changedistributiondb (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributiondb_TSQL
- sp_changedistributiondb
helpviewer_keywords:
- sp_changedistributiondb
ms.assetid: 66f73185-ea9e-43f9-86ed-9dd933cee2f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 031fc14eba8cdea8cdbff41d18d6e6ab6bc42a68
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133848"
---
# <a name="spchangedistributiondb-transact-sql"></a>sp_changedistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更散發資料庫的屬性。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changedistributiondb [ @database= ] 'database'   
    [ , [ @property= ] 'property' ]   
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@database=**] **'**_資料庫_**'**  
 這是散發資料庫的名稱。 *資料庫*已**sysname**，沒有預設值。  
  
 [  **@property=**] **'**_屬性_**'**  
 這是給定資料庫要變更的屬性。 *屬性*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**history_retention**|記錄資料表保留期限。|  
|**max_distretention**|最大散發保留期限。|  
|**min_distretention**|最小散發保留期限。|  
|NULL (預設值)|所有可用*屬性*值會列印。|  
  
 [  **@value=**] **'**_值_**'**  
 這是指定之屬性的新值。 *值*已**nvarchar(255)**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedistributiondb**用於所有類型的複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/sp-changedistributiondb-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changedistributiondb**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
