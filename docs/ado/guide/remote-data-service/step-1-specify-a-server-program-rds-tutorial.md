---
title: 步驟1：指定伺服器程式（RDS 教學課程） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b7856a6a77720b4988c4a15afd86f24ff0070b28
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764689"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>步驟 1：指定伺服器程式 (RDS 教學課程)
在最常見的情況下，請使用[RDS。](../../../ado/reference/rds-api/dataspace-object-rds.md)[使用者空間] 物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法，指定預設伺服器程式、 [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)或您自己的自訂伺服器程式（商務物件）。 伺服器程式會在伺服器上具現化，並傳回伺服器程式或*proxy*的參考。  
  
 本教學課程使用預設的伺服器程式：  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [步驟2：叫用伺服器程式（RDS 教學課程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
