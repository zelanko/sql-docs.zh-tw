---
title: "網際網路伺服器錯誤： 拒絕存取 |Microsoft 文件"
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
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0338761d1fbd9991185959cfcac4d54746fb6ebb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="internet-server-error-access-denied"></a>網際網路伺服器錯誤： 存取遭拒
如果您收到這個錯誤，通常表示 Microsoft 網際網路資訊服務 (IIS) 會傳回下列狀態：  
  
 HTTP_STATUS_DENIED 401  
  
 請確定 IIS 所存取的目錄有適當的權限。 RDS 可以與任何一種三種密碼驗證模式執行的 IIS Web 伺服器進行通訊： 匿名、 基本或 NT 挑戰/回應 （在 Windows 2000 中稱為整合式 Windows 驗證）。 此外，Web 伺服器必須具有與資料來源電腦的權限，如果它是 NT/Windows 2000年的電腦。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)





