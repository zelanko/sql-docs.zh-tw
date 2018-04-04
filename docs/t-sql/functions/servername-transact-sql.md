---
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 40f441998f2f5055bdacb0ac6d796a6d3ad56f68
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機伺服器名稱。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 在安裝期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會將伺服器名稱設成電腦名稱。 若要變更伺服器的名稱，請使用 **sp_addserver**，然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 當安裝多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，如果本機伺服器名稱在安裝之後不曾改變，@@SERVERNAME 會傳回下列本機伺服器名稱資訊。  
  
|執行個體|伺服器資訊|  
|--------------|------------------------|  
|預設執行個體|'*servername*'|  
|具名執行個體|'*servername*\\*instancename*'|  
|容錯移轉叢集執行個體 - 預設執行個體|'*virtualservername*'|  
|容錯移轉叢集執行個體 - 具名執行個體|'*virtualservername*\\*instancename*'|  
  
 雖然 @@SERVERNAME 函式和 SERVERPROPERTY 函式的 SERVERNAME 屬性可能傳回具有類似格式的字串，但資訊可能不同。 SERVERNAME 屬性會自動報告電腦網路名稱的變更。  
  
 相反地，@@SERVERNAME 並不會報告這類變更。 @@SERVERNAME 會報告利用 **sp_addserver** 或 **sp_dropserver** 預存程序來進行的本機伺服器名稱變更。  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何使用 `@@SERVERNAME`。  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 範例結果集如下：  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
