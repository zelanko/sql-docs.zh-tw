---
title: "SortDirection 屬性 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- SortDirection property [RDS]
ms.assetid: 1d9d8715-e4ad-4ff3-bf7f-f1dc0532d8c2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d0395c390da04314dad0bc886f71333baac7b7a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sortdirection-property-rds"></a>SortDirection 屬性 (RDS)
表示排序順序為遞增或遞減。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SortDirection = value  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *值*  
 A**布林**值，當設定為**True**，表示為遞增排序方向。 **False**表示遞減順序。  
  
## <a name="remarks"></a>備註  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， **SortDirection**， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)屬性會提供排序和篩選功能，用戶端快取。 排序功能會使用一個資料行值排序記錄。 篩選功能會顯示在完整的尋找準則的所有記錄的子集[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)維護快取中。 [重設](../../../ado/reference/rds-api/reset-method-rds.md)方法會執行準則和取代目前**資料錄集**具有可更新**資料錄集**。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、 FilterCriterion、 FilterValue、 SortColumn，和 SortDirection 屬性及重設方法範例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [排序內容](../../../ado/reference/ado-api/sort-property.md)   
 [SortColumn 屬性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)



