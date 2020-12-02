---
description: STIsEmpty (geometry 資料類型)
title: STIsEmpty (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsEmpty_TSQL
- STIsEmpty (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsEmpty (geometry Data Type)
ms.assetid: dcbd6ae1-5d63-485f-9d58-28bfd504524e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1a03f368cbb462abf668af25a0c01c662f1ec199
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445054"
---
# <a name="stisempty-geometry-data-type"></a>STIsEmpty (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

如果 **geometry** 執行個體是空的，便傳回 1。 如果 **geometry** 執行個體不是空的，則傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsEmpty ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="examples"></a>範例  
 下列範例會建立空的 `geometry` 例項，並使用 `STIsEmpty()` 來測試看看此例項是不是空的。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON EMPTY', 0);  
SELECT @g.STIsEmpty();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

