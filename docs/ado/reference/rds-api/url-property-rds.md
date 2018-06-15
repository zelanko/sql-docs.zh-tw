---
title: URL 屬性 (RDS) |Microsoft 文件
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb07f83de6f08202b80da6a56bcf781510eb237f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288807"
---
# <a name="url-property-rds"></a>URL 屬性 (RDS)
表示字串，包含相對或絕對的 URL。  
  
 您可以設定**URL**屬性在設計階段於[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在執行階段在指令碼中。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>參數  
 *Server*  
 A**字串**包含有效的 URL 值。  
  
 *DataControl*  
 物件變數，表示**DataControl**物件。  
  
## <a name="remarks"></a>備註  
 一般而言，此 URL 會識別 Active Server Page (.asp) 檔案，可以產生並傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 因此，使用者可以取得**資料錄集**而不用叫用伺服器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件，或撰寫自訂的商務物件。  
  
 如果**URL**屬性已設定， [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)會將變更提交至由 URL 指定的位置。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [URL 屬性範例 (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


