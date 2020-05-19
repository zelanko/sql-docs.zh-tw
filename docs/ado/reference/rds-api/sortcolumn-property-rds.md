---
title: SortColumn 屬性（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: rothja
ms.author: jroth
ms.openlocfilehash: 83975a46087f75d58be304c543f6e6a45b6db7e6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750841"
---
# <a name="sortcolumn-property-rds"></a>SortColumn 屬性 (RDS)
指出要排序記錄的資料行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *字串*  
 **字串**值，表示用來排序記錄之資料行的名稱或別名。  
  
## <a name="remarks"></a>備註  
 **SortColumn**、 [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md)、 [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md)、 [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)和[FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)屬性提供用戶端快取的排序和篩選功能。 排序功能會依據一個資料行的值來排序記錄。 篩選功能會根據尋找準則顯示記錄的子集，而完整的[記錄集會](../../../ado/reference/ado-api/recordset-object-ado.md)保留在快取中。 [Reset](../../../ado/reference/rds-api/reset-method-rds.md)方法會執行準則，並以可更新的**記錄集**取代目前的**記錄集**。  
  
 若要排序**記錄集**，您必須先儲存任何暫止的變更。 如果您使用**RDS。DataControl**，您可以使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法。 例如，如果您的**RDS。DataControl**的名稱為 ADC1，您的程式碼會是 `ADC1.SubmitChanges` 。 如果您使用的是 ADO**記錄集**，則可以使用其[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用**UpdateBatch**是使用[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法所建立之**記錄集**物件的建議方法。 例如，您的程式碼可以是 `myRS.UpdateBatch` 或 `ADC1.Recordset.UpdateBatch` 。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 屬性和 Reset 方法範例（VBScript）](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort 屬性](../../../ado/reference/ado-api/sort-property.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





