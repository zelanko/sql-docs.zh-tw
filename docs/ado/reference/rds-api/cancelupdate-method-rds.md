---
title: CancelUpdate 方法（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: rothja
ms.author: jroth
ms.openlocfilehash: 05426b2d4fba81e70a8bae35db215bcd750d3169
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746343"
---
# <a name="cancelupdate-method-rds"></a>CancelUpdate 方法 (RDS)
取消對[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的目前或新資料列所做的任何變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 OLE DB 的資料指標服務會保留原始值和變更快取的複本。 當您呼叫**CancelUpdate**時，變更的快取會重設為空白，而且任何繫結控制項都會以原始資料重新整理。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [CancelUpdate 方法範例（VBScript）](../../../ado/reference/rds-api/cancelupdate-method-example-vbscript.md)   
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Refresh 方法（RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


