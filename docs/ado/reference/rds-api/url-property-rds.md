---
description: URL 屬性 (RDS)
title: " (RDS) 的 URL 屬性 |Microsoft Docs"
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: rothja
ms.author: jroth
ms.openlocfilehash: 5f0db677fcd63e3532553f0051ba88930d0f5c8a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767267"
---
# <a name="url-property-rds"></a>URL 屬性 (RDS)
指出包含相對或絕對 URL 的字串。  
  
 您可以在設計階段于[DataControl](./datacontrol-object-rds.md)物件的物件標記，或在腳本程式碼的執行時間設定**URL**屬性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>參數  
 *Server*  
 包含有效 URL 的 **字串** 值。  
  
 *DataControl*  
 代表 **DataControl** 物件的物件變數。  
  
## <a name="remarks"></a>備註  
 URL 通常會識別使用中的伺服器頁 ( .asp) 檔案，該檔案可以產生並傳回 [記錄集](../ado-api/recordset-object-ado.md)。 因此，使用者可以取得 **記錄集** ，而不需要叫用伺服器端 [DataFactory](./datafactory-object-rdsserver.md) 物件，或編寫自訂商務物件。  
  
 如果已設定 **url** 屬性， [SubmitChanges](./submitchanges-method-rds.md) 會將變更提交至 url 所指定的位置。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [URL 屬性範例 (VBScript)](./url-property-example-vbscript.md)