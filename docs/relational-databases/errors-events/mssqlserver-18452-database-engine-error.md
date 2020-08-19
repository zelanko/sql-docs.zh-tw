---
description: MSSQLSERVER_18452
title: MSSQLSERVER_18452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
- 18452 (Database Engine error)
ms.assetid: 21da332c-e81d-4dee-a9d2-95598911b3be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0704998c40476ae040d3f8263ab3a47b1817f1e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385654"
---
# <a name="mssqlserver_18452"></a>MSSQLSERVER_18452
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|18452|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOGON_INVALID_CONNECT|  
|訊息文字|使用者 '%.*ls' 的登入失敗。 此登入為 SQL Server 登入，不能用於 Windows 驗證。%.\*ls|  
  
## <a name="explanation"></a>說明  
使用者嘗試使用無法驗證的認證進行登入。 可能的原因包括：  
  
-   此登入可能是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，但是伺服器只接受 Windows 驗證。  
  
-   您正嘗試使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接，但是所使用的登入不存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。  
  
-   此登入可能使用 Windows 驗證，但是此登入是無法辨識的 Windows 主體。 無法辨識的 Windows 主體是表示 Windows 無法驗證此登入。 這可能是因為 Windows 登入來自於不受信任的網域。  
  
類似的問題可能會導致較常見的錯誤 18456。  
  
## <a name="user-action"></a>使用者動作  
如果您正嘗試使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接，請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是在混合驗證模式下設定。  
  
如果您正嘗試使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接，請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入存在。  
  
如果您正嘗試使用 Windows 驗證進行連接，請確定您已適當地登入正確的網域。  
  
