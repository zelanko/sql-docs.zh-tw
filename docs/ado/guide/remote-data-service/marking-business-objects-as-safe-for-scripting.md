---
description: 將商務物件標示為可安全編寫指令碼
title: 將商務物件標示為安全的腳本 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: rothja
ms.author: jroth
ms.openlocfilehash: 2cbbfaba540f5349fb7cc0291b8259eeda5b0d68
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978049"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>將商務物件標示為可安全編寫指令碼
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 為了協助確保安全的網際網路環境，您必須標記任何以 RDS 具現化的商務物件 [。](../../reference/rds-api/dataspace-object-rds.md) 以「安全的方式撰寫腳本」的空間物件 [CreateObject](../../reference/rds-api/createobject-method-rds.md) 方法。 您必須確保在系統登錄的授權區域中將它們標示為如此，才可在 DCOM 中使用。  
  
> [!NOTE]
>  標示為「安全的腳本」或「安全進行初始化」的商務物件可以透過網路上的任何人來具現化及初始化。 將商務物件標示為「安全的腳本」，並不會讓它安全。 請務必確定商務物件是以最高的安全性編寫程式碼，以確保這類物件不會針對機密資料呈現未受保護的存取點。  
  
 若要手動將您的商務物件標示為安全的腳本，請建立包含下列文字的 .reg 副檔名的文字檔。 在此範例中， \<*MyActiveXGUID*> 是您商務物件的十六進位 GUID 號碼。 下列兩個數字啟用安全腳本功能：  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 使用登錄編輯程式儲存檔案，並將其合併到您的登錄中，或按兩下 Windows 檔案總管中的 .reg 檔案。  
  
 在 Microsoft Visual Basic 中建立的商務物件，可以使用 [封裝和部署嚮導] 自動標示為「安全的腳本」。 當 wizard 要求您指定安全性設定時，請選取 [ **安全的初始化** 和 **安全] 以編寫腳本**。  
  
 在最後一個步驟中，[應用程式安裝程式] 會建立 .htm 和 .cab 檔。 然後，您可以將這兩個檔案複製到目的電腦，然後按兩下 .htm 檔案以載入頁面，並正確地註冊伺服器。  
  
 由於商務物件預設會安裝在 Windows\System32\Occache 目錄中，因此請將它移至 Windows\System32 目錄，並變更**HKEY_CLASSES_ROOT 的 \clsid \\ **InprocServer32 登錄機 \<*MyActiveXGUID*> \\ **InprocServer32**碼，使其符合正確的路徑。