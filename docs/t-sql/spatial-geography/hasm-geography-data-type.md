---
title: HasM (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9ece3c57981f52b1359f40d59487c464b6c5a230
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852853"
---
# <a name="hasm-geography-data-type"></a>HasM (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

如果空間物件至少包含一個 M 值，則傳回 1 (true)，否則傳回 0 (false)。  
  
## <a name="syntax"></a>語法  
  
```sql  
  
.HasM  
```  
  
## <a name="return-types"></a>傳回類型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
CLR 傳回類型：**布林**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>範例  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理執行個體上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
