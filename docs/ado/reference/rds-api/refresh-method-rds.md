---
title: 重新整理方法 (RDS) |Microsoft 文件
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89e9088aeec78213f7da9a79ba78255de4b94b97
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="refresh-method-rds"></a>重新整理方法 (RDS)
重新查詢中指定的資料來源[連接](../../../ado/reference/rds-api/connect-property-rds.md)屬性和更新的查詢結果。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
## <a name="remarks"></a>備註  
 您必須設定[連接](../../../ado/reference/rds-api/connect-property-rds.md)，[伺服器](../../../ado/reference/rds-api/server-property-rds.md)，和[SQL](../../../ado/reference/rds-api/sql-property.md)屬性才能使用**重新整理**方法。 與相關聯的表單上的所有資料繫結控制項**.RDSDataControl**物件會反映新的記錄集。 已存在的任何[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)釋放物件，並會捨棄任何未儲存的變更。 **重新整理**方法會自動將第一筆記錄目前的記錄。  
  
 最好呼叫**重新整理**方法定期當您使用的資料。 如果您擷取資料，並再將它用戶端電腦上，保留一段時間，則可能會變成過期。 有可能，您所做的任何變更將會失敗，因為其他人可能已變更的記錄和送出之前，您的變更。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [重新整理方法範例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [重新整理方法範例 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [地址通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [重新整理方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


