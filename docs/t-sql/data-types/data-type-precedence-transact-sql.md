---
description: 資料類型優先順序 (Transact-SQL)
title: 資料類型優先順序 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6ed8d2a30d4bcc2cd1adaedc3cccd6642d701533
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459920"
---
# <a name="data-type-precedence-transact-sql"></a>資料類型優先順序 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md.md](../../includes/tsql-appliesto-ss2012-all-md.md)]

當一個運算子結合不同資料類型的運算式時，低優先順序資料類型會先轉換為高優先順序資料類型。 如果轉換不是支援的隱含轉換，就會傳回錯誤。 若運算子結合的運算元運算式具有相同資料類型，則作業結果就含有該資料類型。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用下列資料類型優先順序：
  
1.  使用者自訂資料類型 (最高)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **date**  
1. **time**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **text**  
1. **image**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (包含 **nvarchar(max)**)  
1. **nchar**  
1. **varchar** (包含 **varchar(max)**)  
1. **char**  
1. **varbinary** (包含 **varbinary(max)**)  
1. **binary** (最低)  
  
## <a name="see-also"></a>另請參閱
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
