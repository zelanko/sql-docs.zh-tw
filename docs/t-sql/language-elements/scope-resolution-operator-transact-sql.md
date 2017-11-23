---
title: ":: （範圍解析) (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4fa0fa1cd5a86ab4dc736803f6d4926b98f4a30
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="-scope-resolution-transact-sql"></a>:: （範圍解析) (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  範圍解析運算子**::**存取複合資料類型的靜態成員。 複合資料類型是指包含多個簡單資料類型和方法，例如內建的 CLR 型別和自訂 SQLCLR User-Defined 型別 (Udt)。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用範圍解析運算子來存取 `GetRoot()` 類型的 `hierarchyid` 成員。  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>請參閱＜  
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
