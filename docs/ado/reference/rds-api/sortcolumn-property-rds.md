---
description: SortColumn 屬性 (RDS)
title: SortColumn 屬性 (RDS) |Microsoft Docs
ms.technology: ado
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
ms.openlocfilehash: 62187b1643c315099d40d0bdd878699fcfc0065c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724225"
---
# <a name="sortcolumn-property-rds"></a>SortColumn 屬性 (RDS)
指出排序記錄的資料行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](./datacontrol-object-rds.md) 物件。  
  
 *String*  
 **字串**值，表示用來排序記錄之資料行的名稱或別名。  
  
## <a name="remarks"></a>備註  
 **SortColumn**、 [SortDirection](./sortdirection-property-rds.md)、 [FilterValue](./filtervalue-property-rds.md)、 [FilterCriterion](./filtercriterion-property-rds.md)和[FilterColumn](./filtercolumn-property-rds.md)屬性提供用戶端快取上的排序和篩選功能。 排序功能會依據一個資料行的值來排序記錄。 篩選功能會根據尋找準則顯示記錄的子集，而完整的 [記錄集會](../ado-api/recordset-object-ado.md) 保留在快取中。 [Reset](./reset-method-rds.md)方法會執行準則，並將目前的**記錄集**取代為可更新的**記錄集**。  
  
 若要排序 **記錄集**，您必須先儲存任何暫止的變更。 如果您使用 **RDS。DataControl**，您可以使用 [SubmitChanges](./submitchanges-method-rds.md) 方法。 例如，如果您的 **RDS。DataControl** 名為 ADC1，您的程式碼會是 `ADC1.SubmitChanges` 。 如果您使用的是 ADO **記錄集**，可以使用它的 [UpdateBatch](../ado-api/updatebatch-method.md) 方法。 使用**UpdateBatch**是使用[CreateRecordset](./createrecordset-method-rds.md)方法所建立的**記錄集**物件的建議方法。 例如，您的程式碼可以是 `myRS.UpdateBatch` 或 `ADC1.Recordset.UpdateBatch` 。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [FilterColumn、FilterCriterion、FilterValue、SortColumn 和 SortDirection 屬性以及 Reset 方法範例 (VBScript) ](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort 屬性](../ado-api/sort-property.md)   
 [SortDirection 屬性 (RDS)](./sortdirection-property-rds.md)