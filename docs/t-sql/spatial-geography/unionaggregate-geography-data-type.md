---
title: UnionAggregate (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UnionAggregate
- UnionAggregate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geography)
ms.assetid: 1a3aeef1-5b0e-4ae8-aeb7-c4aab22f42ab
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b445c6ff9b5e182bed9f0b5860d6ac00b2634051
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689576"
---
# <a name="unionaggregate-geography-data-type"></a>UnionAggregate (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

在一組地理物件上執行聯集作業。
  
## <a name="syntax"></a>語法  
  
```  
  
UnionAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>引數  
 *geography_operand*  
 這是 **geography** 類型資料表資料行，可保留要在其上執行聯集作業的一組 **geography** 物件。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
## <a name="remarks"></a>Remarks  
 如果輸入具有不同的 SRID，方法會傳回 **null**。 請參閱[空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
 此方法會忽略 **null** 輸入。  
  
> [!NOTE]  
>  如果所有輸入的值都為 **null**，此方法就會傳回 **null**。  
  
## <a name="examples"></a>範例  
 下列範例會在城市內的一組 **geography** 位置點上執行 `UnionAggregate`。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::UnionAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
