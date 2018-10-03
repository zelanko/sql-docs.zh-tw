---
title: ':: (範圍解析) (Transact-SQL) | Microsoft Docs'
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
ms.openlocfilehash: 74cc0fbbe0d3eeae2637ca7c91ba28e531abbf22
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711766"
---
# <a name="-scope-resolution-transact-sql"></a>:: (範圍解析) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  範圍解析運算子 **::** 可讓您存取複合資料類型的靜態成員。 複合資料類型包含多個簡單資料類型和方法，例如內建的 CLR 類型和自訂的 SQLCLR 使用者定義類型 (UDT)。  
  
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
  
  
