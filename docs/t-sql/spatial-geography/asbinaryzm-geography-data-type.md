---
title: "AsBinaryZM (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AsBinaryZM
- AsBinaryZM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM, geography
- AsBinaryZM
ms.assetid: 37246adb-814d-4113-9983-4d336de8182c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 99981d95095b97dd599787578f891a39e60098ac
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="asbinaryzm-geography-data-type"></a>AsBinaryZM (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回開放式地理空間協會 (OGC) 已知二進位 (well-known binary，WKB) 表示**幾何**執行個體夾帶任何**Z** （高度） 和**M** （量值）執行個體所夾帶的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **varbinary （max)**  
  
 CLR 傳回類型： **SqlBytes**  
  
## <a name="remarks"></a>備註  
  
## <a name="examples"></a>範例  
  
```sql  
DECLARE @g1 GEOGRAPHY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M & #40; geography 資料類型 & #41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z & #40; geography 資料類型 & #41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
