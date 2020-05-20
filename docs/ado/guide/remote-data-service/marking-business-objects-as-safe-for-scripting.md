---
title: 將商務物件標示為安全的腳本 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a6655b1bba274a9dc5079c7c996b58da6ba8ae0f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763599"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>將商務物件標示為可安全編寫指令碼
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 為了協助確保安全的網際網路環境，您必須將任何以 RDS 具現化的商務物件標示為[。](../../../ado/reference/rds-api/dataspace-object-rds.md)以「安全地進行腳本處理」的空間物件[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 您必須確保它們在系統登錄的 [授權] 區域中被標示為，然後才能在 DCOM 中使用。  
  
> [!NOTE]
>  標示為「安全進行腳本處理」或可安全進行初始化的商務物件，可以透過網路上的任何人進行具現化及初始化。 將商務物件標示為「安全地進行腳本處理」並不會使其安全。 務必確保商務物件的編碼具有最高的安全性，以確保這類物件不會針對機密資料呈現未受保護的存取點。  
  
 若要手動將您的商務物件標示為可安全編寫腳本，請建立副檔名為 .reg 的文字檔，其中包含下列文字。 在此範例中， \< *MyActiveXGUID*> 是您商務物件的十六進位 GUID 編號。 下列兩個數字可啟用安全的腳本功能：  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 儲存檔案，然後使用 [登錄編輯程式] 或按兩下 Windows Explorer 中的 .reg 檔案，將它合併到您的登錄中。  
  
 在 Microsoft Visual Basic 中建立的商務物件可以使用封裝和部署嚮導，自動標示為「安全地進行腳本處理」。 當嚮導要求您指定安全性設定時，請選取 [**安全] 進行初始化**，並**提供 [安全] 進行腳本**處理。  
  
 在最後一個步驟中，應用程式安裝精靈會建立 .htm 和 .cab 檔案。 接著，您可以將這兩個檔案複製到目的電腦，然後按兩下 .htm 檔案以載入頁面，並正確地註冊伺服器。  
  
 因為商務物件預設會安裝在 Windows\System32\Occache 目錄中，所以請將它移至 Windows\System32 目錄，並將**HKEY_CLASSES_ROOT \\ \clsid** \< *MyActiveXGUID* > \\ **InprocServer32**登錄機碼變更為符合正確的路徑。


