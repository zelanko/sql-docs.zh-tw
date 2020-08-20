---
description: sp_dropdistributor (Transact-SQL)
title: sp_dropdistributor (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 404ef0654abde8b9d41659d7dd25bf80ac5b3bb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469566"
---
# <a name="sp_dropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  解除安裝散發者。 這個預存程序執行於散發資料庫以外任何資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @no_checks = ] no_checks` 指出在卸載散發者之前，是否要檢查相依物件。 *no_checks* 是 **bit**，預設值是0。  
  
 如果是 **0**， **sp_dropdistributor** 檢查以確定除了散發者之外，所有發行和散發物件都已卸載。  
  
 如果是 **1**， **sp_dropdistributor** 會在卸載散發者之前，先卸載所有的發行和散發物件。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否在未連接到散發者的情況下執行此預存程式。 *ignore_distributor* 是 **bit**，預設值是 **0**。  
  
 如果是 **0**， **sp_dropdistributor** 會連接到散發者，並移除所有的複寫物件。 如果 **sp_dropdistributor** 無法連接到散發者，預存程式就會失敗。  
  
 如果是 **1**，就不會對散發者進行連接，而且不會移除複寫物件。 如果在解除安裝散發者，或散發者已永久離線，便使用這個項目。 在未來重新安裝散發者之前，不會移除這個發行者在散發者的物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropdistributor** 用於所有類型的複寫中。  
  
 如果伺服器上有其他發行者或散發物件存在，除非** \@ no_checks**設定為**1**，否則**sp_dropdistributor**會失敗。  
  
 您必須執行 **sp_dropdistributiondb**，以卸載散發資料庫之後，才會執行這個預存程式。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_dropdistributor**。  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
