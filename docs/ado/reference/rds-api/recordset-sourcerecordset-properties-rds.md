---
title: Recordset、SourceRecordset 屬性（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0cca4735e65ce5d96d431fa455181de921e4474
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963576"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset、SourceRecordset 屬性 (RDS)
表示從自訂商務物件傳回的**記錄集**物件。  
  
 **適用于：** [DATACONTROL 物件（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *Recordset*  
 代表**記錄集**物件的物件變數。  
  
## <a name="remarks"></a>備註  
 您可以將**SourceRecordset**屬性設定為自訂商務物件所傳回的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 這些屬性可讓應用程式透過自訂進程來處理系結進程。 它們會接收包裝在**記錄集中**的資料列集，讓您可以直接與**記錄集**互動，執行設定屬性或逐一查看**記錄集**的動作。  
  
 您可以在執行時間的腳本程式碼中，設定**SourceRecordset**屬性或讀取**記錄集**屬性。  
  
 **SourceRecordset**是一個僅限寫入的屬性，與**記錄集**屬性相反，這是唯讀屬性。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 和 SourceRecordset 屬性範例（VBScript）](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 方法（RDS）](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query 方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


