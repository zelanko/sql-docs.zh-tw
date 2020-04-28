---
title: FetchOptions 屬性（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e4e0943a675ef7cf3684ccddd2699fba02dac9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964128"
---
# <a name="fetchoptions-property-rds"></a>FetchOptions 屬性 (RDS)
表示非同步提取的類型。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="setting-and-return-values"></a>設定和傳回值  
 設定或傳回下列其中一個值。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adcFetchUpFront**|將控制權傳回給應用程式之前，會提取[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的所有記錄。 在允許應用程式對其執行任何動作之前，會先提取完整的**記錄集**。|  
|**adcFetchBackground**|一旦提取記錄的第一個批次之後，控制項就可以返回應用程式。 後續讀取記錄**集**時，如果嘗試存取未提取在第一個批次中的記錄，將會延遲到實際提取記錄為止，此時控制項會回到應用程式。|  
|**adcFetchAsync**|預設值。 當記錄在背景中提取時，控制項會立即返回應用程式。 如果應用程式嘗試讀取尚未提取的記錄，則會讀取最接近搜尋記錄的記錄，且控制權會立即傳回，表示已達到**記錄集**目前的結尾。 例如， [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)的呼叫會將目前的記錄位置移至實際提取的最後一筆記錄，即使有更多的記錄會繼續填入**記錄集**也一樣。|  
  
> [!NOTE]
>  每個使用這些常數的用戶端可執行檔都必須提供宣告給它們。 您可以從位於 RDS 程式庫的預設安裝資料夾中的 Adcvbs 檔案，剪下並貼上您想要的常數宣告。  
  
## <a name="remarks"></a>備註  
 在 Web 應用程式中，您通常會想要使用**adcFetchAsync** （預設值），因為它會提供更好的效能。 在編譯的用戶端應用程式中，您通常會想要使用**adcFetchBackground**。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例（VBScript）](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


