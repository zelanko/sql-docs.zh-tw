---
title: "步驟 1： 指定程式的伺服器 （RDS 教學課程） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c79cf47179f8fff140f4fda779b5db816c1d9418
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>步驟 1： 指定程式的伺服器 （RDS 教學課程）
在最常見的案例中，使用[.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法，以指定的預設伺服器程式， [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，或您自己自訂的伺服器程式 （商務物件）。 伺服器程式具現化伺服器，以及伺服器程式的參考上或*proxy*，就會傳回。  
  
 本教學課程會使用預設伺服器程式：  
  
```  
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [步驟 2： 叫用伺服器程式 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

