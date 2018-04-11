---
title: 處理常式屬性 (RDS) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa363b9fa9761eb764a7bf2aa7b9d4eb992ec65b
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="handler-property-rds"></a>處理常式屬性 (RDS)
表示延伸功能的伺服器端自訂程式 （處理常式） 的名稱[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，以及使用任何參數*處理常式*。  
  
 **適用於：** [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>參數  
 *DataControl*  
 物件變數，表示[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 *字串*  
 A**字串**所有以逗號分隔值，其中包含的處理常式和任何參數，名稱 (例如， `"handlerName,parm1,parm2,...,parm` *N*`"`)。  
  
## <a name="remarks"></a>備註  
 此屬性支援[自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)，需要設定的功能[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**。  
  
 處理常式，其參數的名稱在的話，會以逗號分隔 （"，"）。 如果分號，系統就會產生無法預期的行為 （";"） 內顯示的任何地方*字串*。 您可以撰寫自己的處理常式，前提是它支援**IDataFactoryHandler**介面。  
  
 預設處理常式名稱是**MSDFMAP。處理常式**，且其預設參數是名為自訂檔案**MSDFMAP。INI**。 您可以使用這個屬性來叫用您的伺服器管理員所建立的替代自訂檔案。  
  
 設定的替代方案**處理常式**屬性是指定的處理常式中與參數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性; 也就是"**處理常式 = * * * handlerName，parameter1，...; parameter2*".  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [處理常式屬性範例 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


