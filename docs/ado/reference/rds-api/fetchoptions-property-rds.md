---
description: FetchOptions 屬性 (RDS)
title: FetchOptions 屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: rothja
ms.author: jroth
ms.openlocfilehash: cee86b2d579a02d9e6cbcc06bfa5d95714f1ecd9
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722309"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 屬性 (RDS)
表示非同步提取的型別。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="setting-and-return-values"></a>設定和傳回值  
 設定或傳回下列其中一個值。  
  
|常數|描述|  
|--------------|-----------------|  
|**adcFetchUpFront**|系統會先提取 [記錄集](../ado-api/recordset-object-ado.md) 的所有記錄，然後再將控制權傳回給應用程式。 完整的 **記錄集會** 先提取，才能讓應用程式使用它來執行任何動作。|  
|**adcFetchBackground**|一旦提取第一個批次的記錄，控制項就可以返回應用程式。 後續的 **記錄集** 讀取嘗試存取未在第一個批次中提取的記錄，將會延遲到實際提取提取的記錄為止，此時控制權會返回應用程式。|  
|**adcFetchAsync**|預設值。 在背景中提取記錄時，控制項會立即返回應用程式。 如果應用程式嘗試讀取尚未提取的記錄，將會讀取最接近搜尋記錄的記錄，且控制權會立即傳回，表示已達到 **記錄集** 的目前結尾。 例如，呼叫 [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 會將目前的記錄位置移至實際提取的最後一筆記錄，即使有更多記錄仍將繼續填入 **記錄集**也是一樣。|  
  
> [!NOTE]
>  使用這些常數的每個用戶端可執行檔都必須提供宣告。 您可以從 Adcvbs 檔案中，剪下並貼上您想要的常數宣告（位於 RDS 程式庫的預設安裝資料夾中）。  
  
## <a name="remarks"></a>備註  
 在 Web 應用程式中，您通常會想要使用 **adcFetchAsync** (預設值) ，因為它提供更好的效能。 在編譯的用戶端應用程式中，您通常會想要使用 **adcFetchBackground**。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例 (VBScript) ](./executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](./cancel-method-rds.md)