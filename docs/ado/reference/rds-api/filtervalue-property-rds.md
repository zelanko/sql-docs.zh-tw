---
description: FilterValue 屬性 (RDS)
title: FilterValue 屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: rothja
ms.author: jroth
ms.openlocfilehash: 7afa3fbe785c5b625ba64f4494d45d5f362e0ce7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982129"
---
# <a name="filtervalue-property-rds"></a>FilterValue 屬性 (RDS)
指出用來篩選記錄的值。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](./datacontrol-object-rds.md) 物件。  
  
 *String*  
 **字串**值，表示用來篩選記錄的資料值，例如 (， `'Programmer'` 或 `125`) 。  
  
## <a name="remarks"></a>備註  
 [SortColumn](./sortcolumn-property-rds.md)、 [SortDirection](./sortdirection-property-rds.md)、 **FilterValue**、 [FilterCriterion](./filtercriterion-property-rds.md)和[FilterColumn](./filtercolumn-property-rds.md)屬性提供用戶端快取上的排序和篩選功能。 排序功能會依據一個資料行的值來排序記錄。 篩選功能會根據尋找準則顯示記錄的子集，而完整的 [記錄集會](../ado-api/recordset-object-ado.md) 保留在快取中。 [Reset](./reset-method-rds.md)方法會執行準則，並將目前的**記錄集**取代為可更新的**記錄集**。  
  
 Null 值會導致類型不符的錯誤。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 屬性以及 Reset 方法範例 (VBScript) ](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 屬性 (RDS) ](./filtercolumn-property-rds.md)   
 [FilterCriterion 屬性 (RDS) ](./filtercriterion-property-rds.md)   
 [SortColumn 屬性 (RDS) ](./sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](./sortdirection-property-rds.md)