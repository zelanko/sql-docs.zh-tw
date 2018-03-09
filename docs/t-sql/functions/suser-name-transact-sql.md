---
title: "SUSER_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cb236dc3ae7f74ad77ba398e328d4a0bf93a079b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  傳回使用者的登入識別名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>引數  
 *server_user_id*  
 這是使用者的登入識別碼。 *server_user_id*，這就是選擇性的是**int**。*server_user_id*可以是任何登入識別碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 使用者或群組是否有權限連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*server_user_id*是未指定，會傳回目前使用者的登入識別名稱。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版中，安全性識別碼 (SID) 取代了伺服器使用者識別碼 (SUID)。  
  
 SUSER_NAME 傳回僅針對具有項目中的登入的登入名稱**syslogins**系統資料表。  
  
 SUSER_NAME 可用在選取清單、WHERE 子句及任何允許使用運算式的位置中，且後面一律必須接著括號，即使未指定任何參數也是如此。  
  
## <a name="examples"></a>範例  
 下列範例會傳回登入識別碼是 `1` 之使用者的登入識別名稱。  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [SUSER_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/suser-id-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
