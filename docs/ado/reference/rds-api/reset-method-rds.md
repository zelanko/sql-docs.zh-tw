---
title: "Reset 方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4762d331c76b1e97d13ffd1dbf926a35468bcaa9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="reset-method-rds"></a>Reset 方法 (RDS)
用戶端上執行排序或篩選**資料錄集**根據指定的排序和篩選屬性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *value*  
 選擇性。 A**布林**值為**True** （預設值） 如果您想要篩選目前的 「 篩選 」 資料列集。 **False**指出您想要篩選原始資料列集上移除任何先前的篩選選項。  
  
## <a name="remarks"></a>備註  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)， [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)， [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)， [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)，和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)屬性會提供排序和篩選功能，用戶端快取。 排序功能的訂單記錄中有一個資料行的值。 篩選功能會顯示根據搜尋準則，同時完整記錄的子集[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)維護快取中。 **重設**方法會執行準則和取代目前**資料錄集**具有可更新**資料錄集**。  
  
 如果沒有不已送出，原始資料的變更**重設**方法將會失敗。 首先，使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法來儲存任何變更，在讀取/寫入**資料錄集**，然後使用**重設**方法來排序或篩選的記錄。  
  
 如果您想要在您的資料列集上執行一個以上的篩選器，您可以使用選擇性*布林*引數與**重設**方法。 下列範例會示範如何執行這項操作：  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>請參閱＜  
 [FilterColumn、 FilterCriterion、 FilterValue、 SortColumn，和 SortDirection 屬性及重設方法範例 (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



