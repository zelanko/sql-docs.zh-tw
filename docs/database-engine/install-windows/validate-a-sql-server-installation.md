---
title: 驗證 SQL Server 安裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: bda8d393f0563879d009191599ed9e124a5c2eb7
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40412733"
---
# <a name="validate-a-sql-server-installation"></a>驗證 SQL Server 安裝

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 探索報告可以用於驗證電腦上所安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 [已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告] 會顯示安裝在本機伺服器上之所有 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)] 產品及功能的報告。 您可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心的 **工具** 頁面存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告。  
  
 ## <a name="run-includessnoversionincludesssnoversion-mdmd-features-discovery-report"></a>執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告  
  
 如果要啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心，請使用 [開始] 功能表，並依序指向 [所有程式]、[[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<版本名稱>] 和 [組態工具]，然後按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心]。 如果要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告，請按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心] 左側導覽區域中的 [工具]，然後按一下 [已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能探索報告]。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 探索報告會儲存在 %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<最後一個安裝程式工作階段\>。  
  
 您也可以從命令列產生探索報告。 請從命令提示字元執行 "Setup.exe /Action=RunDiscovery"。如果您在上述命令列中新增 "/q"，則不會顯示 UI，但仍會在 %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<最後一個安裝程式工作階段\> 中建立報表。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
