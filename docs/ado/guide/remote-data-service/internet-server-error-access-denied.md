---
title: 網際網路伺服器錯誤： 存取遭到拒絕 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b7c562e57341dd027a4cd9bdc3a0fa4bbe51ae5
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558391"
---
# <a name="internet-server-error-access-denied"></a>網際網路伺服器錯誤：拒絕存取
如果您收到這個錯誤，通常表示 Microsoft 網際網路資訊服務 (IIS) 會傳回下列狀態：  
  
 HTTP_STATUS_DENIED 401  
  
 請確定 IIS 所存取的目錄有適當的權限。 RDS 可與執行中的三種密碼驗證模式的任何一個 IIS Web 伺服器通訊： 匿名、 基本或 NT Challenge/Response （稱為 Windows 2000 中的整合式 Windows 驗證）。 此外，Web 伺服器必須具有資料來源電腦上的權限，如果它是 Windows NT/Windows 2000 的電腦。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)




