---
description: FilterColumn 屬性 (RDS)
title: FilterColumn 屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterColumn property [ADO]
ms.assetid: 0a5473e8-8ce6-4518-83fb-4920b827e285
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d86d772d14150b09992433648a24994f14fc9df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439000"
---
# <a name="filtercolumn-property-rds"></a>FilterColumn 屬性 (RDS)
表示用來評估篩選準則的資料行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.FilterColumn = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 物件。  
  
 *String*  
 **字串**值，指定要在其中評估篩選準則的資料行。 篩選準則是在 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md) 屬性中指定的。  
  
## <a name="remarks"></a>備註  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)和**FilterColumn**屬性提供用戶端快取上的排序和篩選功能。 排序功能會依據一個資料行的值來排序記錄。 篩選功能會根據尋找準則顯示記錄的子集，而完整的 [記錄集會](../../../ado/reference/ado-api/recordset-object-ado.md) 保留在快取中。 [Reset](../../../ado/reference/rds-api/reset-method-rds.md)方法會執行準則，並將目前的**記錄集**取代為可更新的**記錄集**。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 屬性以及 Reset 方法範例 (VBScript) ](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterCriterion 屬性 (RDS) ](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [FilterValue 屬性 (RDS) ](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 屬性 (RDS) ](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


