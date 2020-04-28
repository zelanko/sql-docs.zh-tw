---
title: 網際網路伺服器錯誤：拒絕存取 |Microsoft Docs
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
ms.openlocfilehash: adbfc4e56c49447d88fb354d1e67c2c5e3e30b71
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922628"
---
# <a name="internet-server-error-access-denied"></a>網際網路伺服器錯誤：拒絕存取
如果您收到此錯誤，通常表示 Microsoft Internet Information Services （IIS）傳回下列狀態：  
  
 HTTP_STATUS_DENIED 401  
  
 請確定 IIS 存取的目錄具有適當的許可權。 RDS 可以與下列三種密碼驗證模式中的任何一個執行的 IIS Web 服務器通訊：匿名、基本或 NT 挑戰/回應（在 Windows 2000 中稱為整合式 Windows 驗證）。 此外，如果 Web 服務器是 Windows NT/Windows 2000 電腦，則必須擁有資料來源電腦的許可權。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)




