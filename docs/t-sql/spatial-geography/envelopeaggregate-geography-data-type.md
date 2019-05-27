---
title: EnvelopeAggregate (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a14ffb001e82757fba2f7557aed3d374142bb99b
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937904"
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回一組指定 **geography** 物件的週框物件。 產生的 **geography** 物件包含多個圓弧線段。
  
## <a name="syntax"></a>語法  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>引數  
 *geography_operand*  
 這是 **geography** 類型資料表資料行，可保存要執行封套彙總作業的一組 **geography** 物件。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
## <a name="remarks"></a>Remarks  
 如果產生的週框物件大於半球，則會傳回 **FullGlobe** 物件。 這個方法並不精確。  
  
 如果輸入具有不同的 SRID，方法會傳回 **null**。 請參閱[空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)。  
  
 此方法會忽略 **null** 輸入。  
  
> [!NOTE]  
>  如果所有輸入的值都為 **null**，此方法就會傳回 **null**。  
  
## <a name="examples"></a>範例  
 下列範例會在城市內的一組 **geography** 位置點上執行 `EnvelopeAggregate`。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
