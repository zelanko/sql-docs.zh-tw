---
title: "InternetTimeout 屬性 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2320ba200cf8343a32e2a0d00589a80014517260
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="internettimeout-property-rds"></a>InternetTimeout 屬性 (RDS)
表示要要求逾時前等候毫秒的數。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**逾時的值，表示要求之前的毫秒數。  
  
## <a name="remarks"></a>備註  
 這個屬性只適用於要求的 HTTP 或 HTTPS 通訊協定來傳送。  
  
 三層環境中的要求可能需要幾分鐘才能執行。 使用這個屬性來指定更多長時間執行要求的時間。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[資料空間物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|  
  
## <a name="see-also"></a>另請參閱  
 [InternetTimeout 屬性範例 (VB)](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout 屬性範例 （VC + +）](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 


