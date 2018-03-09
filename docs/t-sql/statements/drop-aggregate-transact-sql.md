---
title: "卸除彙總 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f01299f0a5db2ed47975a964104e720cb7c8c52
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除使用者自訂的彙總函式。 使用者定義彙總函式會建立使用[CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>引數  
 *IF EXISTS*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有當它已經存在有條件地卸除彙總。  
  
 *schema_name*  
 這是使用者定義彙總函式所屬的結構描述名稱。  
  
 *aggregate_name*  
 這是您要卸除的使用者定義彙總函式的名稱。  
  
## <a name="remarks"></a>備註  
 若有任何檢視、函數或預存程序是利用參考您要卸除之使用者定義彙總函式的結構描述繫結所建立，就不會執行 DROP AGGREGATE。  
  
## <a name="permissions"></a>Permissions  
 若要執行 DROP AGGREGATE，使用者至少必須對使用者自訂彙總所屬的結構描述具備 ALTER 權限，或是對彙總具備 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會卸除彙總 `Concatenate`。  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [建立使用者定義彙總](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
