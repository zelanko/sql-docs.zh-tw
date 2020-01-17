---
title: 連接至另一部電腦 (SQL Server 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 03f409e11e037fcc406940d5a97e9934a77b96b4
ms.sourcegitcommit: c98c6e33d04d4a1888db7dbe89cb0b1bb3a66418
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2019
ms.locfileid: "74249762"
---
# <a name="scm-services---connect-to-another-computer"></a>SCM 服務 - 連接至另一台電腦

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 連線到另一部電腦。 請遵循第一個程序，開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (mmc) 中的 Windows [電腦管理]，並連接到該電腦，然後展開 [服務與應用程式] 樹狀目錄。 請遵循第二個程序，在遠端電腦上建立連結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的檔案。

> [!NOTE]
> 從遠端連線時，有些動作 Configuration Manager 無法執行。

若要啟動、停止、暫停或繼續另一台電腦上的服務，您也可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]連接到伺服器，並以滑鼠右鍵按一下伺服器或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，然後按一下所要的動作。

## <a name="SSMSProcedure"></a>

### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>若要以 Windows 電腦管理連接到另一部電腦

1. 以滑鼠右鍵按一下 [開始]  功能表，然後按一下 [電腦管理 (本機)]  。
2. 在 [動作]  功能表上，按一下 [連線到另一台電腦]  。
3. 在 [選取電腦]  對話方塊的 [另一台電腦]  文字方塊中，輸入要管理的電腦名稱，然後按一下 [確定]  。

   [電腦管理] 會顯示出遠端電腦上執行的服務。 最上層節點會變更為 [電腦管理 \< 遠端電腦 >]   。

4. 在主控台樹狀目錄中，展開 [服務與應用程式]  ，然後展開 [SQL Server 組態管理員]  ，來管理遠端電腦的服務。

### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>若要儲存另一台電腦的 SQL Server 組態管理員連結

1. 在 **[開始]** 功能表上，按一下 **[執行]** 。

2. 在 [開啟]  方塊中，輸入 **mmc -a** (或在 64 位元電腦中輸入 **mmc /32 -a**)，以作者模式開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console。
3. 在 [檔案]  功能表上，按一下 [新增/移除嵌入式管理單元]  。
4. 在 [新增/移除嵌入式管理單元]  視窗中，按一下 [新增]  。
5. 在 [新增獨立嵌入式管理單元]  視窗中，依序按一下 [電腦管理]  和 [新增]  。
6. 在 [電腦管理]  視窗中，按一下 [另一台電腦]  ，並輸入想要管理之遠端電腦的名稱，然後按一下 [完成]  。
7. 在 [新增獨立嵌入式管理單元]  視窗中，按一下 [關閉]  。
8. 在 [新增/移除嵌入式管理單元]  視窗中，按一下 [確定]  。
9. 依序展開 [電腦管理 (\<電腦名稱>)]    和 [服務與應用程式]  。
10. 以滑鼠右鍵按一下 [SQL Server 組態管理員]  ，然後按一下 [從這裡新增視窗]  。
11. 在 [視窗]  功能表上，按一下 [主控台根目錄]  ，以切換回第一個視窗，並刪除該視窗。
12. 在 [檔案]  功能表上，按一下 [另存新檔]  ，並將檔案以副檔名為 **.msc** 的適當名稱儲存在所要的資料夾中。 請關閉 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console。
13. 若要在目標電腦上開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請按兩下該檔案。 如果想要，也請將檔案的連結儲存在桌面或 [開始]  功能表中。

> [!CAUTION]
> 在遠端電腦上使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員時，電腦名稱並不明顯，且可能會錯誤地停止或設定錯誤的電腦。 在 [服務]  索引標籤上，核取 [主機名稱]  方塊，以便在修改服務之前確認電腦名稱。

## <a name="see-also"></a>另請參閱

- [設定 WMI 在 SQL Server 工具中顯示伺服器狀態](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)
