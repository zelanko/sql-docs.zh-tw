---
title: "FilterCriterion 屬性 (RDS) |Microsoft 文件"
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
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b30e26e6584e6895185eb67ceb7824ae7323cea
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="filtercriterion-property-rds"></a>FilterCriterion 屬性 (RDS)
表示要使用篩選器值中的評估運算子。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *字串*  
 A**字串**值，指定評估運算子的[FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)的記錄。 可以是下列其中一個： <， \<=、 >、 > =、 =、 或 <>。  
  
## <a name="remarks"></a>備註  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， **FilterCriterion**，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)屬性會提供排序和篩選功能，用戶端快取。 排序功能的訂單記錄中有一個資料行的值。 篩選功能會顯示在完整的尋找準則的所有記錄的子集[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)維護快取中。 [重設](../../../ado/reference/rds-api/reset-method-rds.md)方法會執行準則和取代目前**資料錄集**具有可更新**資料錄集**。  
  
 "！ ="運算子不是有效值**FilterCriterion**; 相反地，使用"<>"。  
  
 如果設定篩選和排序屬性，而且您呼叫**重設**方法，先篩選資料列集並排序然後。 表示遞增排序，null 值會在頂端。遞減排序，null 值都在底端 （遞增是預設行為）。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、 FilterCriterion、 FilterValue、 SortColumn，和 SortDirection 屬性及重設方法範例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn 屬性 (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue 屬性 (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn 屬性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)



