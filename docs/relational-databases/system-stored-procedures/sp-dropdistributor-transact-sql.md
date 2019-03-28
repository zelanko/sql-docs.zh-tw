---
title: sp_dropdistributor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f1a1baec088af48cd18972c177463fbb3f574eb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530680"
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  解除安裝散發者。 這個預存程序執行於散發資料庫以外任何資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @no_checks = ] no_checks` 指出是否要卸除 「 散發者 」 之前檢查相依物件。 *no_checks*已**元**，預設值是 0。  
  
 如果**0**， **sp_dropdistributor**會檢查以確認除了散發者端的發行和散發物件，已卸除。  
  
 如果**1**， **sp_dropdistributor**卸除然後再解除安裝散發者端的所有發行和散發物件。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否要將此預存程序執行而不需要連線到散發者。 *ignore_distributor*已**位元**，預設值是**0**。  
  
 如果**0**， **sp_dropdistributor**會連接到 「 散發者 」，並移除所有複寫物件。 如果**sp_dropdistributor**無法連接到散發者 」，則預存程序會失敗。  
  
 如果**1**，不會連接到散發者 」 並不會移除複寫物件。 如果在解除安裝散發者，或散發者已永久離線，便使用這個項目。 在未來重新安裝散發者之前，不會移除這個發行者在散發者的物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdistributor**用於所有類型的複寫。  
  
 如果在伺服器上的其他發行者或散發物件存在**sp_dropdistributor**會失敗，除非**@no_checks**設為**1**。  
  
 藉由執行卸除散發資料庫之後，就必須執行這個預存程序**sp_dropdistributiondb**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_dropdistributor**。  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
