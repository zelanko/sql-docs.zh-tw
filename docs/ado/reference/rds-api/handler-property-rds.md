---
title: Handler 屬性（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: rothja
ms.author: jroth
ms.openlocfilehash: 22e054a6f1723f32d81a4f00ec941a10f8212506
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751942"
---
# <a name="handler-property-rds"></a>Handler 屬性 (RDS)
指示伺服器端自訂程式（處理常式）的名稱，這個程式會擴充[RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)的功能，以及*處理常式*所使用的任何參數。  
  
 **適用于：** [DATACONTROL 物件（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 代表 RDS 的物件變數[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *字串*  
 包含處理常式名稱和任何參數的**字串**值，全都以逗號分隔（例如 `"handlerName,parm1,parm2,...,parm` *N* `"` ）。  
  
## <a name="remarks"></a>備註  
 這個屬性支援[自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)，這是需要將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**的功能。  
  
 處理常式及其參數的名稱（如果有的話）會以逗號（"，"）分隔。 如果*字串*中的任何位置出現分號（";"），則會產生無法預期的行為。 您可以撰寫自己的處理常式，前提是它支援**IDataFactoryHandler**介面。  
  
 預設處理常式的名稱是**MSDFMAP。處理常式**和其預設參數是名為 MSDFMAP 的自訂檔案 **。INI**。 使用此屬性可叫用伺服器系統管理員所建立的替代自訂檔案。  
  
 設定**處理常式**屬性的替代方法是在[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性中指定處理常式和參數。也就是 "**Handler =**_handlerName，parameter1，parameter2,...;_"。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Handler 屬性範例（VB）](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


