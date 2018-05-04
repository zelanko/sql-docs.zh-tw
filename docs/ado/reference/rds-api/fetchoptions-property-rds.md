---
title: FetchOptions 屬性 (RDS) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe754d9fe91818e0f80a4b027e3bf74aae11bfeb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 屬性 (RDS)
表示非同步擷取的類型。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="setting-and-return-values"></a>設定和傳回值  
 設定或傳回下列值之一。  
  
|常數|Description|  
|--------------|-----------------|  
|**adcFetchUpFront**|所有記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)控制項傳回至應用程式之前提取。 完整**資料錄集**之前執行任何動作，它允許應用程式擷取。|  
|**adcFetchBackground**|控制項可以傳回至應用程式儘速擷取第一個批次的記錄。 後續的讀取**資料錄集**，嘗試存取未擷取第一個批次中的記錄將會延遲，直到實際擷取大的記錄，此時控制項會傳回給應用程式。|  
|**adcFetchAsync**|預設值。 控制權立即交還給應用程式時在背景中擷取的記錄。 如果應用程式會嘗試讀取尚未尚未擷取的記錄，將讀取的最大記錄的記錄，並控制會立即傳回，表示目前結尾**資料錄集**已達到。 例如，若要呼叫[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)會實際擷取，最後一筆記錄來移動目前的記錄位置，即使多的記錄會繼續擴展**資料錄集**。|  
  
> [!NOTE]
>  這些常數會使用每個用戶端可執行檔必須提供它們的宣告。 您可以剪下並貼上您想要從檔案 Adcvbs.inc，位於 RDS 程式庫的預設安裝資料夾的常數宣告。  
  
## <a name="remarks"></a>備註  
 在 Web 應用程式中，您通常想要使用**adcFetchAsync** （預設值），因為它提供更佳的效能。 在已編譯的用戶端應用程式中，您通常想要使用**adcFetchBackground**。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


