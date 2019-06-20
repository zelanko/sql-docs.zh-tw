---
title: 伺服器屬性 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7b23466adb660f2aa18cb44a20d189f456c3bb3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697543"
---
# <a name="server-property-rds"></a>Server 屬性 (RDS)
指出 Internet Information Services (IIS) 名稱和通訊的通訊協定。  
  
 您可以設定**伺服器**屬性，在設計階段中的物件標記[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，或在執行階段在指令碼中。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 **HTTP**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 執行階段語法  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 執行階段語法  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 執行階段語法  
  
```  
  
DataControl.Server="computername"  
```  
  
 **同處理序**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 執行階段語法  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>參數  
 *awebsrvr*或*computername*  
 A**字串**包含網際網路或內部網路路徑或電腦名稱，如果伺服器是在遠端電腦，或空字串，如果伺服器是在本機電腦上的值。  
  
 *port*  
 選擇性。 用來連接到執行 IIS 的伺服器連接埠。 在 Internet Explorer 中設定的連接埠號碼 (在**檢視** 功能表中，按一下**選項**，然後選取**連接** 索引標籤) 或在 IIS 中。  
  
 *DataControl*  
 物件變數，表示**rds。DataControl**物件。  
  
## <a name="remarks"></a>備註  
 伺服器是位置其中**rds。DataControl**處理要求 （也就是查詢或更新）。 根據預設，所有的要求會由處理[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件， [MSDFMAP。處理常式](../../../ado/guide/remote-data-service/datafactory-customization.md)元件，和[MSDFMAP。INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)指定的伺服器上的檔案。 請記住，變更要協調設定中的舊和新的伺服器時**MSDFMAP。INI**檔案。 不相容性可能會成功的要求導致無法在另一部伺服器上。 如果 [伺服器] 屬性設定為空字串""，這些物件會使用本機電腦上。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [伺服器屬性範例 (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [連接屬性 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL 屬性](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


