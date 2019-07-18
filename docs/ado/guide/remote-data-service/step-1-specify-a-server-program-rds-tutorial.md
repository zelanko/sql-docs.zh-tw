---
title: 步驟 1：指定的伺服器程式 （RDS 教學課程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6cecddfe127bba43852412b6d804254f35103def
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922112"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>步驟 1：指定伺服器程式 (RDS 教學課程)
在最常見的案例中，使用[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法，以指定預設 server 計畫[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，或您自己自訂的伺服器程式 （商務物件）。 伺服器程式具現化伺服器和伺服器程式的參考或*proxy*，則會傳回。  
  
 本教學課程會使用預設伺服器程式：  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [步驟 2：叫用伺服器程式 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
