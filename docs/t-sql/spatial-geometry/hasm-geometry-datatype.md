---
title: HasM (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ab164bf204b7fa7d65e5a8a879422a95b208f0ec
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/25/2019
ms.locfileid: "56800962"
---
# <a name="hasm-geometry-datatype"></a>HasM (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果空間物件至少包含一個 M 值，則傳回 1 (true)，否則傳回 0 (false)。  
  
## <a name="syntax"></a>語法  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**布林**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>範例  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何執行個體上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  