---
title: "IsNull (geometry 資料類型) | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2017
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
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e13c3df72687ccee0d684d97cebe41737fbecbbb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="isnull-geometry-data-type"></a>IsNull (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**geometry** 執行個體的類型為 Null。 如果此例項不是 Null，就會傳回 0。
  
## <a name="syntax"></a>語法  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**bit**  
  
 CLR 類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull` 可用來測試 **geometry** 執行個體是否為 Null。 這會產生令人混淆的結果，當此例項不是 Null 時傳回 0，但是如果此例項為 Null 則傳回 Null。  
  
 這個方法主要是由 SQL Server 基礎結構所使用；不建議您使用 `IsNull` 來測試例項是否為 Null。  
  

## <a name="see-also"></a>另請參閱  
 [幾何例項上擴充的方法](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

