---
title: "Cancel 方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b742549444f1348ebbadd1328147694b5f85a94e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="cancel-method-rds"></a>Cancel 方法 (RDS)
取消執行暫止狀態，非同步方法呼叫。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>備註  
 當您呼叫**取消**， [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md)會自動設為**adcReadyStateLoaded**，而[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)會是空白。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [取消方法範例 (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [ExecuteOptions 屬性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


