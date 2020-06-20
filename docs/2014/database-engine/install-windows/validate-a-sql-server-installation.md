---
title: 驗證 SQL Server 安裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8dd4e6ce7800c3a0a9db51f6c1a4bddfe7a188c3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931689"
---
# <a name="validate-a-sql-server-installation"></a>驗證 SQL Server 安裝
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 探索報告可以用於驗證電腦上所安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 [**已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告**] 會顯示 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安裝在本機伺服器上之所有、、、、和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 產品及功能的報告。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心的 **工具** 頁面存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告。  
  
 **若要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告：**  
  
 啟動 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心]，使用 [**開始**] 功能表，依序指向 [**所有程式**]、 ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name> **[] 和 [**組態工具**]，然後按一下 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心**]。 如果要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告，請按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心] 左側導覽區域中的 [工具]，然後按一下 [已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告]。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]探索報告已儲存至% ProgramFiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<上一個安裝程式會話 \> 。  
  
 您也可以從命令列產生探索報告。 從命令提示字元執行 "Setup.exe/Action = RunDiscovery"。如果您在上述命令列中新增 "/q"，則不會顯示 UI，但仍會在% ProgramFiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<最後一個安裝程式會話 \> 中建立報表。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](view-and-read-sql-server-setup-log-files.md)  
  
  
