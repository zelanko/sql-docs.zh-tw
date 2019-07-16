---
title: 標示為安全的商務物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55ae560f35a06e77803bfb011f4d430d5079ea05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922600"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>將商務物件標示為可安全編寫指令碼
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要協助確保安全的網際網路環境，您需要具現化任何商務物件標示[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件的[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法為 「 指令碼的安全。 」 您需要確保它們會如此標示，在系統登錄的授權區域之前可用於 DCOM。  
  
> [!NOTE]
>  商務物件標示為 「 安全指令碼處理 」 或安全的初始化可以具現化並初始化任何人都在網路上。 將商務物件標示為 「 安全指令碼處理 」 不會進行其安全。 它是非常重要，藉此確定商務物件會具有最高的安全性，以確保這類物件不會顯示未受保護的存取點的敏感性資料編碼。  
  
 若要以手動方式標記您的商務物件為安全的指令碼，建立副檔名為.reg，其中包含下列文字的文字檔案。 在此範例中， \< *MyActiveXGUID*> 是您的商務物件的十六進位 GUID 數字。 下列兩個數字會啟用安全的-指令碼的功能：  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 儲存檔案，並將其合併到您的登錄中，使用登錄編輯程式，或按兩下 Windows 檔案總管中的.reg 檔案。  
  
 建立 Microsoft Visual Basic 中的商務物件可以自動標示為 「 安全指令碼處理 」 與套件及部署精靈。 時精靈會要求您指定安全性設定，選取**安全可供初始化**並**安全用於指令碼**。  
  
 在最後一個步驟中，應用程式安裝精靈會建立.htm 和.cab 檔案。 然後您可以將這兩個檔案複製到目標電腦，並按兩下.htm 檔案，以載入該頁面，並正確登錄伺服器。  
  
 因為商務物件將會安裝 Windows\System32\Occache 目錄中，依預設，將它移到 Windows\System32 目錄，並變更**HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32**登錄機碼，以符合正確的路徑。


