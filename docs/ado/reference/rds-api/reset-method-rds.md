---
title: Reset 方法（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c2f40460a4690e32cb3f94963c8cbc1f7f06c15
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750987"
---
# <a name="reset-method-rds"></a>Reset 方法 (RDS)
根據指定的排序和篩選屬性，在用戶端**記錄集**上執行排序或篩選。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *值*  
 選擇性。 **布林**值，如果您想要篩選目前的「已篩選」資料列集，則為**True** （預設值）。 **False**表示您會篩選原始資料列集，並移除任何先前的篩選選項。  
  
## <a name="remarks"></a>備註  
 [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md)、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)屬性提供用戶端快取的排序和篩選功能。 排序功能會依據一個資料行的值來排序記錄。 篩選功能會根據尋找準則顯示記錄的子集，而完整的[記錄集會](../../../ado/reference/ado-api/recordset-object-ado.md)保留在快取中。 **Reset**方法會執行準則，並以可更新的**記錄集**取代目前的**記錄集**。  
  
 如果原始資料的變更尚未提交，**重設**方法將會失敗。 首先，使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法來儲存讀取/寫入**記錄集中**的任何變更，然後使用**Reset**方法來排序或篩選記錄。  
  
 如果您想要在資料列集上執行多個篩選，您可以使用選擇性的*布林值*引數搭配**Reset**方法。 下列範例示範如何執行：  
  
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
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 屬性和 Reset 方法範例（VBScript）](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



