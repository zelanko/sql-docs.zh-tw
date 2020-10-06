---
description: Recordset、SourceRecordset 屬性 (RDS)
title: 記錄集、SourceRecordset 屬性 (RDS) |Microsoft Docs
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cdf8a894341343fee7576daed45c75a46857b909
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724295"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset、SourceRecordset 屬性 (RDS)
表示從自訂商務物件傳回的 **記錄集** 物件。  
  
 **適用于：** [DATACONTROL 物件 (RDS) ](./datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](./datacontrol-object-rds.md) 物件。  
  
 *Recordset*  
 代表 **記錄集** 物件的物件變數。  
  
## <a name="remarks"></a>備註  
 您可以將 **SourceRecordset** 屬性設定為自訂商務物件傳回的 [記錄集](../ado-api/recordset-object-ado.md) 。  
  
 這些屬性可讓應用程式透過自訂進程來處理系結程式。 它們會接收包裝在 **記錄集中** 的資料列集，如此您就可以直接與 **記錄集**互動，執行設定屬性或逐一查看 **記錄集**的動作。  
  
 您可以設定 **SourceRecordset** 屬性，或在執行時間以腳本處理常式代碼來讀取 **記錄集** 屬性。  
  
 **SourceRecordset** 是僅限寫入的屬性，相較于 **記錄集** 屬性是唯讀屬性。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 和 SourceRecordset 屬性範例 (VBScript) ](./recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [RDS)  (CreateRecordset 方法 ](./createrecordset-method-rds.md)   
 [Query 方法 (RDS)](./query-method-rds.md)