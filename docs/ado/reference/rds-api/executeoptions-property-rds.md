---
description: ExecuteOptions 屬性 (RDS)
title: ExecuteOptions 屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fe38de33ea0b5f0784af27f031d2a93759d15aa
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722354"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 屬性 (RDS)
指出是否已啟用非同步執行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列其中一個值。  
  
|常數|描述|  
|--------------|-----------------|  
|**adcExecSync**|以同步方式執行下次重新整理 [記錄集](../ado-api/recordset-object-ado.md) 。|  
|**adcExecAsync**|預設值。 以非同步方式執行下次重新整理 **記錄集** 。|  
  
> [!NOTE]
>  使用這些常數的每個可執行檔都必須提供宣告。 您可以從 Adcvbs 檔案中，剪下並貼上您想要的常數宣告（位於 RDS 程式庫的預設安裝資料夾中）。  
  
## <a name="remarks"></a>備註  
 如果 **ExecuteOptions** 設定為 **adcExecAsync**，則會以非同步方式在 RDS 上 **執行下次重新** 整理呼叫 [。DataControl](./datacontrol-object-rds.md) 物件的 **記錄集**。  
  
 如果您嘗試在另一個可能變更 RDS 的非同步作業時，呼叫 [Reset](./reset-method-rds.md)、 [Refresh](./refresh-method-rds.md)、 [SubmitChanges](./submitchanges-method-rds.md)、 [CancelUpdate](../ado-api/cancelupdate-method-ado.md)或 [Recordset](./recordset-sourcerecordset-properties-rds.md) [。](./datacontrol-object-rds.md) 正在執行 DataControl 物件的 **記錄集** ，發生錯誤。  
  
 如果非同步作業期間發生錯誤，則為 **RDS。DataControl** 物件的 [ReadyState](./readystate-property-rds.md) 值會從 **adcReadyStateLoaded** 變更為 **adcReadyStateComplete**，而且 **記錄集** 屬性值不會維持 *Nothing*。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例 (VBScript) ](./executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](./cancel-method-rds.md)