---
title: "為 FILESTREAM 存取設定防火牆 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbaaa631770966cff9cafa15fffb60b24dcd2767
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="configure-a-firewall-for-filestream-access"></a>為 FILESTREAM 存取設定防火牆
  若要在受防火牆保護的環境中使用 FILESTREAM，用戶端和伺服器都必須能夠將 DNS 名稱解析為包含 FILESTREAM 檔案的伺服器。 FILESTREAM 要求 Windows 檔案共用通訊埠 139 和 445 必須要開啟。  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>在執行 Windows 7 的電腦上開啟 Windows 檔案共用通訊埠  
  
1.  在 [控制台] 中，開啟 [Windows 防火牆]。  
  
2.  在左窗格中，按一下 [進階設定]。 若是系統提示需要管理員密碼或確認，請輸入密碼或提供確認。  
  
3.  在 [具有進階安全性的 Windows 防火牆] 對話方塊的左窗格中，按一下 [輸入規則]，然後按一下右窗格中的 [新增規則]。  
  
4.  遵循 [新增輸入規則精靈] 中的指示以加入 TCP 通訊埠 139。  
  
5.  重複上一個步驟以加入 TCP 通訊埠 445。  
  
6.  關閉 [具有進階安全性的 Windows 防火牆] 對話方塊。  
  
  
