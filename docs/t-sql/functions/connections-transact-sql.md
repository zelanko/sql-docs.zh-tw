---
title: "@@CONNECTIONS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8422da0d4e550c99fac6c9659f771ab98196cb4a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;連接 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上次啟動之後所嘗試的連接次數，成功和失敗都包括在內。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>傳回型別
**integer**
  
## <a name="remarks"></a>備註  
連接次數並不等於使用者數目。 例如，當沒有觀察連接的使用者時，應用程式仍可以開啟多個通往 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接。
  
若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]統計資料，包括連接嘗試，執行**sp_monitor**。
  
@@MAX_CONNECTIONS 是同時允許伺服器的連線數目上限。 @@CONNECTIONS 會隨著每次登入嘗試，因此 @@CONNECTIONS 可能大於 @@MAX_CONNECTIONS 。
  
## <a name="examples"></a>範例  
下列範例會顯示傳回迄今 (到目前的日期和時間為止) 的登入嘗試次數。
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>另請參閱
[系統統計函數 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  
