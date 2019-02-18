---
title: ::(範圍解析) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2e6e7d28fb4b04b61c1cd1cf5877d231f220e76
ms.sourcegitcommit: 5ef24b3229b4659ede891b0af2125ef22bd94b96
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2019
ms.locfileid: "55759941"
---
# <a name="-scope-resolution-transact-sql"></a>::(範圍解析) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  範圍解析運算子 **::** 可讓您存取複合資料類型的靜態成員。 複合資料類型包含了多個簡單的資料類型和方法。 複合資料類型包括所內建 CLR 類型和自訂的 SQLCLR 使用者定義型別 (UDT)。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用範圍解析運算子來存取 `GetRoot()` 類型的 `hierarchyid` 成員。  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
 