---
title: "ExecuteOptions 屬性 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76876c9182ccba3eab0fa8f16171a3dceabd0876
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="executeoptions-property-rds"></a>ExecuteOptions 屬性 (RDS)
指出是否已啟用非同步執行。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列值之一。  
  
|常數|描述|  
|--------------|-----------------|  
|**adcExecSync**|執行在下次重新整理[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)同步。|  
|**adcExecAsync**|預設值。 執行在下次重新整理**資料錄集**以非同步的方式。|  
  
> [!NOTE]
>  每個使用這些常數的可執行檔必須提供它們的宣告。 您可以剪下並貼上您想要從檔案 Adcvbs.inc，位於 RDS 程式庫的預設安裝資料夾的常數宣告。  
  
## <a name="remarks"></a>備註  
 如果**ExecuteOptions**設**adcExecAsync**，則這會以非同步方式執行下一個**重新整理**上呼叫[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**資料錄集**。  
  
 如果您嘗試呼叫[重設](../../../ado/reference/rds-api/reset-method-rds.md)，[重新整理](../../../ado/reference/rds-api/refresh-method-rds.md)， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)，或[資料錄集](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)而另一項非同步作業，可能會變更[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**資料錄集**正在執行時，發生錯誤。  
  
 如果非同步作業期間，發生錯誤**.RDSDataControl**物件的[ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)值變更從**adcReadyStateLoaded**至**adcReadyStateComplete**，而**資料錄集**屬性值仍然維持*Nothing*。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>請參閱  
 [ExecuteOptions 和 FetchOptions 屬性範例 (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


