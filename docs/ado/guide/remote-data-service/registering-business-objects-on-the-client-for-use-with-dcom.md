---
title: "使用用戶端上的商務物件向 DCOM |Microsoft 文件"
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
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e293eb58053259dd229656152094763ac31b48a2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>用於搭配 DCOM 用戶端上註冊商務物件
自訂商務物件需要確保用戶端可以將他們的程式名稱 (ProgId) 對應到可透過 DCOM 使用的識別項 (CLSID)。 基於這個理由，DCOM 物件的 ProgID 必須位於用戶端登錄中，並將對應至的伺服器端的商務物件的類別識別碼。 針對其他支援的通訊協定 （HTTP、 HTTPS 和同處理序），這不需要。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果呼叫 MyBObj 與特定的類別識別碼，例如，"{00112233-4455-6677-8899-00AABBCCDDEE}"的伺服器端的商務物件公開 （expose） 請確定下列項目會新增至用戶端登錄：  
  
```  
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```



