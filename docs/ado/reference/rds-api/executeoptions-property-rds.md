---
title: ExecuteOptions 屬性 (RDS) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6ac7ee6c1f996294c1f8aa353719deb11d698e47
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603318"
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 屬性 (RDS)
指出是否已啟用非同步執行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列值之一。  
  
|常數|描述|  
|--------------|-----------------|  
|**adcExecSync**|執行下一步 重新整理[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)同步。|  
|**adcExecAsync**|預設值。 執行下一步 重新整理**資料錄集**以非同步的方式。|  
  
> [!NOTE]
>  每個使用這些常數的可執行檔必須提供它們的宣告。 您可以剪下並貼上您想要從檔案 Adcvbs.inc，位於 預設的安裝資料夾的 RDS 程式庫的常數宣告。  
  
## <a name="remarks"></a>備註  
 如果**ExecuteOptions**設為**adcExecAsync**，則這會以非同步方式執行下一步**重新整理**上呼叫[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**資料錄集**。  
  
 如果您嘗試呼叫[重設](../../../ado/reference/rds-api/reset-method-rds.md)，[重新整理](../../../ado/reference/rds-api/refresh-method-rds.md)， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)，或[資料錄集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)雖然可能會變更的另一個非同步作業[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**資料錄集**正在執行時，發生錯誤。  
  
 如果非同步作業期間，發生錯誤**rds。DataControl**物件的[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)值變更時從**adcReadyStateLoaded**來**adcReadyStateComplete**，而**資料錄集**屬性值仍然維持*Nothing*。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


