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
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62775231"
---
# <a name="validate-a-sql-server-installation"></a>驗證 SQL Server 安裝
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 探索報告可以用於驗證電腦上所安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 [**已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝的功能探索報告**] 會顯示[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]安裝[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]在[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]本地[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]伺服器[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]上之[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]所有、、、、和產品及功能的報告。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心的 **工具** 頁面存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告。  
  
 **若要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行功能探索報告：**  
  
 如果要啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心，請使用 [開始]**** 功能表，並依序指向 [所有程式]****、[**[!INCLUDE[msCoName](../../includes/msconame-md.md)]版本名稱>][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<** 和 [組態工具]****，然後按一下 [** 安裝中心][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**。 如果要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告，請按一下 [** 安裝中心]**** 左側導覽區域中的 [工具][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**，然後按一下 [已安裝的 ** 功能探索報告][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]探索報告已儲存至\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles% \120\Setup Bootstrap\Log\\<上一個安裝程式\>會話。  
  
 您也可以從命令列產生探索報告。 從命令提示字元執行 "setup.exe/Action = RunDiscovery"。如果您在上述命令列中新增 "/q"，則不會顯示 UI，但仍會在\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles% \120\Setup Bootstrap\Log\\中建立報告，<上一個安裝\>程式會話。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](view-and-read-sql-server-setup-log-files.md)  
  
  
