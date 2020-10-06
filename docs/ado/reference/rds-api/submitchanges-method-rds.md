---
description: SubmitChanges 方法 (RDS)
title: " (RDS) 的 SubmitChanges 方法 |Microsoft Docs"
ms.technology: ado
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
ms.openlocfilehash: 69a76648c676af5c6420cffde930ac76c096276d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724172"
---
# <a name="submitchanges-method-rds"></a>SubmitChanges 方法 (RDS)
將本機快取和可更新 [記錄集](../ado-api/recordset-object-ado.md) 的暫止變更提交至 [Connect](./connect-property-rds.md) 屬性或 [URL](./url-property-rds.md) 屬性中所指定的資料來源。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數 [。DataControl](./datacontrol-object-rds.md) 物件。  
  
 *DataFactory*  
 代表 [RDSServer. DataFactory](./datafactory-object-rdsserver.md) 物件的物件變數。  
  
 *[連接]*  
 **字串**值，表示以 RDS 建立的連接 **。DataControl**物件的[Connect](./connect-property-rds.md)屬性。  
  
 *Recordset*  
 代表 **記錄集** 物件的物件變數。  
  
## <a name="remarks"></a>備註  
 [連接](./connect-property-rds.md)、[伺服器](./server-property-rds.md)和[SQL](./sql-property.md)屬性必須先設定，您才能搭配 RDS 使用**SubmitChanges**方法 **。DataControl**物件。  
  
 如果您在呼叫相同**記錄集**物件的**SubmitChanges**之後呼叫[CancelUpdate](./cancelupdate-method-rds.md)方法， **CancelUpdate**呼叫會失敗，因為已認可變更。  
  
 只有變更的記錄會傳送以進行修改，而且所有變更都成功，否則所有變更都會一起失敗。  
  
 您只能使用 **SubmitChanges** 搭配預設的 **RDSServer. DataFactory** 物件。 自訂商務物件不能使用這個方法。  
  
 如果已設定 **url** 屬性， **SubmitChanges** 會將變更提交至 url 所指定的位置。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory 物件 (RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的 SubmitChanges 方法範例 ](./submitchanges-method-example-vbscript.md)   
 [通訊錄命令按鈕](../../guide/remote-data-service/address-book-command-buttons.md)   
 [RDS)  (CancelUpdate 方法 ](./cancelupdate-method-rds.md)   
 [Refresh 方法 (RDS)](./refresh-method-rds.md)