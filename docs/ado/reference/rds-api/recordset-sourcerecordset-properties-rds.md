---
title: "資料錄集 SourceRecordset 屬性 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: feb657674ff4d2d8c17b11246407eaf3fba142d0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="recordset-sourcerecordset-properties-rds"></a>資料錄集 SourceRecordset 屬性 (RDS)
指出**資料錄集**傳回自訂的商務物件的物件。  
  
 **適用於：** [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *資料錄集*  
 物件變數，表示**資料錄集**物件。  
  
## <a name="remarks"></a>備註  
 您可以設定**SourceRecordset**屬性[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從自訂商務物件傳回。  
  
 這些屬性可讓應用程式以處理繫結程序，透過自訂的處理程序。 他們會收到包裝在一個資料列集**資料錄集**，讓您可以直接互動**資料錄集**、 執行動作，例如設定屬性，或逐一**資料錄集**.  
  
 您可以設定**SourceRecordset**屬性或讀取**資料錄集**指令碼在執行階段屬性。  
  
 **SourceRecordset**是唯寫屬性，相對於**資料錄集**屬性，這是唯讀屬性。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>請參閱＜  
 [資料錄集和 SourceRecordset 屬性範例 (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query 方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


