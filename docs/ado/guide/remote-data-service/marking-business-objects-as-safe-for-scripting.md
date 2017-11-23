---
title: "標示為安全的商務物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45f9656022a71deab0cb91a3d9667cbd314c2ffb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>標示為安全的商務物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要協助確保安全的網際網路環境，您要標記以具現化任何商務物件[.RDSDataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法為 「 指令碼的安全。 」 您必須確定它們會如此標示，在系統登錄的授權區域可用於 DCOM 之前。  
  
> [!NOTE]
>  商務物件標示為 「 安全用於指令碼 」 或安全的初始化可以具現化，並在網路上的任何人初始化。 將商務物件標示為 「 安全用於指令碼 」 不會其安全。 它是非常重要，以確定商務物件會以最高的安全性，以確保這類物件不會顯示未受保護的存取點機密資料的自動程式化。  
  
 若要手動標示您的商務物件來編寫指令碼的安全，建立副檔名為.reg，其中包含下列文字的文字檔案。 在此範例中， \< *MyActiveXGUID*> 是您的商務物件的十六進位的 GUID 數字。 下列兩個數字啟用安全的-指令碼的功能：  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 儲存檔案，並使用登錄編輯程式或 Windows 檔案總管 中按兩下.reg 合併到您的登錄。  
  
 建立 Microsoft Visual Basic 中的商務物件可以自動標示為 「 安全用於指令碼 」 與封裝和部署精靈 」。 精靈會要求您指定安全性設定，當選取**安全可供初始化**和**安全用於指令碼**。  
  
 在最後一個步驟中，應用程式安裝精靈會建立為 htm.cab 檔。 您可以將這兩個檔案複製到目標電腦，並按兩下.htm 檔，以載入該頁面，並正確登錄伺服器。  
  
 因為商務物件將會安裝 Windows\System32\Occache 目錄中，依預設，將它移至 Windows\System32 目錄，並變更**HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32**登錄機碼，以符合正確的路徑。


