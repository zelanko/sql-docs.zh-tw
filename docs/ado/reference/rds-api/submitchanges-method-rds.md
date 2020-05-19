---
title: SubmitChanges 方法（RDS） |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a11adb93f3de8f0887eefe964f1c85836ccc43e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750577"
---
# <a name="submitchanges-method-rds"></a>SubmitChanges 方法 (RDS)
將本機快取和可更新[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的暫止變更提交至[Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性或[URL](../../../ado/reference/rds-api/url-property-rds.md)屬性中所指定的資料來源。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *DataFactory*  
 代表[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件的物件變數。  
  
 *建立*  
 **字串**值，表示使用 RDS 建立的連接 **。DataControl**物件的[Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性。  
  
 *Recordset*  
 代表**記錄集**物件的物件變數。  
  
## <a name="remarks"></a>備註  
 您必須先設定[Connect](../../../ado/reference/rds-api/connect-property-rds.md)、 [Server](../../../ado/reference/rds-api/server-property-rds.md)和[SQL](../../../ado/reference/rds-api/sql-property.md)屬性，才能搭配 RDS 使用**SubmitChanges**方法 **。DataControl**物件。  
  
 如果您在呼叫相同**記錄集**物件的**SubmitChanges**後呼叫[CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法， **CancelUpdate**呼叫會失敗，因為變更已經認可。  
  
 只會傳送已變更的記錄進行修改，而且所有變更都會成功，或所有變更都會一起失敗。  
  
 您只能使用**SubmitChanges**搭配預設的**RDSServer. DataFactory**物件。 自訂商務物件無法使用這個方法。  
  
 如果已設定**url**屬性， **SubmitChanges**會將變更提交至 url 所指定的位置。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SubmitChanges 方法範例（VBScript）](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



