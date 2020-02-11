---
title: Server 屬性（RDS） |Microsoft Docs
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
ms.openlocfilehash: 9d196a60986734c5717be9711af1fa28accee414
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963477"
---
# <a name="server-property-rds"></a>Server 屬性 (RDS)
表示 Internet Information Services （IIS）名稱和通訊協定。  
  
 在設計階段，您可以在 RDS 的物件標記中設定**伺服器**屬性[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，或在執行時間的腳本程式碼中。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
 **HTTP**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 執行時間語法  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **IP-HTTPS**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 執行時間語法  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM-IN**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 執行時間語法  
  
```  
  
DataControl.Server="computername"  
```  
  
 **同進程**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 執行時間語法  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>參數  
 *awebsrvr*或*computername*  
 包含網際網路或內部網路路徑的**字串**值; 如果伺服器位於遠端電腦上，則為電腦名稱稱;或者，如果伺服器是在本機電腦上，則為空字串。  
  
 *移植*  
 選擇性。 用來連接到執行 IIS 之伺服器的埠。 埠號碼是在 Internet Explorer 中設定（在 [ **View** ] 功能表上，按一下 [**選項**]，然後選取 [**連接**] 索引標籤）或在 IIS 中。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl**物件。  
  
## <a name="remarks"></a>備註  
 伺服器是 RDS 的位置 **。** 已處理 DataControl 要求（也就是查詢或更新）。 根據預設，所有要求都會由[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件（MSDFMAP）處理[。處理常式](../../../ado/guide/remote-data-service/datafactory-customization.md)元件和[MSDFMAP。](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)指定伺服器上的 INI 檔案。 請記住，變更伺服器以協調舊和新 MSDFMAP 中的設定時 **。INI**檔案。 不相容可能會導致在一部伺服器上成功的要求失敗。 如果伺服器屬性設定為空字串 ""，則會在本機電腦上使用這些物件。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Server 屬性範例（VBScript）](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Connect 屬性（RDS）](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL 屬性](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


