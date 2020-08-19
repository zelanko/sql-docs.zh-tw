---
description: 網際網路伺服器錯誤：拒絕存取
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 970c9c09946cebe74684e6aecc997e56213b1a97
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452170"
---
# <a name="internet-server-error-access-denied"></a>網際網路伺服器錯誤：拒絕存取
如果您收到此錯誤，通常表示 Microsoft Internet Information Services (IIS) 傳回下列狀態：  
  
 HTTP_STATUS_DENIED 401  
  
 請確定 IIS 所存取的目錄具有適當的許可權。 RDS 可以與在下列三種密碼驗證模式中執行的 IIS Web 服務器通訊：匿名、基本或 NT 挑戰/回應 (在 Windows 2000) 中稱為整合式 Windows 驗證。 此外，如果 Web 服務器是 Windows NT/Windows 2000 電腦，則必須具有資料來源電腦的許可權。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)




