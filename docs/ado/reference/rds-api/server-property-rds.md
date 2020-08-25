---
description: Server 屬性 (RDS)
title: Server 屬性 (RDS) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c7d2c095c9f10e95df54849ce729ffdcbbca135
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767517"
---
# <a name="server-property-rds"></a>Server 屬性 (RDS)
指出 Internet Information Services (IIS) 名稱和通訊協定。  
  
 您可以在設計階段于 RDS 的物件標記中設定 **伺服器** 屬性[。DataControl](./datacontrol-object-rds.md) 物件，或在腳本程式碼的執行時間。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
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
  
 **HTTPS**  
  
 設計階段語法  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 執行時間語法  
  
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
 *awebsrvr*或 *computername*  
 包含網際網路或內部網路路徑的 **字串** 值，或電腦名稱稱（如果伺服器位於遠端電腦上）。或者，如果伺服器是在本機電腦上，則為空字串。  
  
 *port*  
 選擇性。 用來連接到執行 IIS 之伺服器的埠。 埠號碼是在 [ **View** ] 功能表的 Internet Explorer (中設定的，按一下 [ **選項**]，然後選取) 或 IIS 中的 [ **連接** ] 索引標籤。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl** 物件。  
  
## <a name="remarks"></a>備註  
 伺服器是 RDS 的位置 **。DataControl** 要求 (也就是處理查詢或更新) 。 依預設，所有要求都是由 [RDSServer. DataFactory](./datafactory-object-rdsserver.md) 物件（MSDFMAP）處理 [。](../../guide/remote-data-service/datafactory-customization.md) 指定之伺服器上的處理常式元件和 [MSDFMAP.INI](../../guide/remote-data-service/understanding-the-customization-file.md) 檔。 請記住，變更伺服器以協調舊的和新的 **MSDFMAP.INI** 檔案中的設定時。 不相容可能會導致一部伺服器上成功的要求失敗。 如果伺服器屬性設定為空字串 ""，就會在本機電腦上使用這些物件。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的伺服器屬性範例 ](./server-property-example-vbscript.md)   
 [連接屬性 (RDS) ](./connect-property-rds.md)   
 [SQL 屬性](./sql-property.md)   
 [SubmitChanges 方法 (RDS)](./submitchanges-method-rds.md)