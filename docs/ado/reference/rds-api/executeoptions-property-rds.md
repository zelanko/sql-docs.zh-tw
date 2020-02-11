---
title: ExecuteOptions 屬性（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ae55ec1fccbd491854fb8bff2daa215d38b20ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964189"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 屬性 (RDS)
指出是否已啟用非同步執行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列其中一個值。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adcExecSync**|以同步方式執行[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的下一次重新整理。|  
|**adcExecAsync**|預設。 以非同步方式執行**記錄集**的下一次重新整理。|  
  
> [!NOTE]
>  使用這些常數的每個可執行檔都必須提供宣告給它們。 您可以從位於 RDS 程式庫的預設安裝資料夾中的 Adcvbs 檔案，剪下並貼上您想要的常數宣告。  
  
## <a name="remarks"></a>備註  
 如果**ExecuteOptions**設定為**adcExecAsync**，則這會以非同步方式在 RDS 上執行下一個**Refresh**呼叫[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**記錄集**。  
  
 如果您嘗試在另一個可能變更 RDS 的非同步作業時，呼叫[Reset](../../../ado/reference/rds-api/reset-method-rds.md)、 [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md)、 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)或[Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) [。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**記錄集**正在執行中，發生錯誤。  
  
 如果非同步作業期間發生錯誤，則為**RDS。DataControl**物件的[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)值會從**adcReadyStateLoaded**變更為**adcReadyStateComplete**，而**記錄集**屬性值*則維持不*變。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例（VBScript）](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


