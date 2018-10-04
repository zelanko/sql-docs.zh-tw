---
title: Recordset、 SourceRecordset 屬性 (RDS) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: bc0b548015cc63117cff566a2c4507b266d5ab7b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657506"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset、SourceRecordset 屬性 (RDS)
指出**資料錄集**從自訂商務物件傳回的物件。  
  
 **適用於：** [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *Recordset*  
 物件變數，表示**資料錄集**物件。  
  
## <a name="remarks"></a>備註  
 您可以設定**SourceRecordset**屬性設[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從自訂商務物件傳回。  
  
 這些內容可讓應用程式以處理透過自訂的處理序的繫結程序。 接到包裝在一個資料列集**Recordset** ，讓您可以直接與互動**資料錄集**、 執行動作，例如設定屬性，或逐一**資料錄集**.  
  
 您可以設定**SourceRecordset**屬性或讀取**資料錄集**指令碼在執行階段的屬性。  
  
 **SourceRecordset**是唯寫屬性，相對於**資料錄集**屬性，這是唯讀的屬性。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 和 SourceRecordset 屬性範例 (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query 方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


