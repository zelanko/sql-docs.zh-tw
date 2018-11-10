---
title: 安裝 SQL Server 2014 服務更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f369185b2d7d5e5d65fc98bca40ba66029ceaa8
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018663"
---
# <a name="install-sql-server-2014-servicing-updates"></a>安裝 SQL Server 2014 服務更新
  本主題提供有關安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]更新的資訊。 本節提供下列作業的相關資訊：  
  
-   在進行新安裝期間安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的更新。  
  
-   在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝完成之後安裝更新。  
  
 我們建議客戶及時評估並安裝最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新，以便確保系統保持在最新狀態而且具有最新的安全性更新。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>在進行新安裝期間安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的更新。  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會整合最新產品更新與主要產品安裝，因此主要產品及其適用的更新可同時安裝。 產品更新可以從下列位置搜尋適用的更新：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   本機資料夾  
  
-   網路共用  
  
 安裝程式找到最新版本的可用更新後，會使用目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序進行下載與整合。 產品更新可能包括累計更新、Service Pack，或 Service Pack 加上累計更新。 產品更新功能是擴充功能[匯集功能](http://go.microsoft.com/fwlink/?LinkId=219945)中所提供之[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]PCU1。  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝完成之後安裝更新  
 在 安裝的執行個體上[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，我們建議您將所有可用的更新： 一般發行版本 (GDR 的安全性/重大更新，) Service Pack (SP)，以及最新可用累積更新 (CU)。  
  
 根據服務發行的類型，SQL Server 更新可透過 Microsoft Update (MU)、 Microsoft 下載中心取得，和/或客戶支援服務 hotfix 伺服器。 （若要能夠看到這些更新，您必須 opt-in 以 MU 透過 Windows Update 控制台 中） 的 Microsoft Update 會自動提供適用於 SQL Server 的安全性和重大更新。 Service Pack 位於 MU 以及 「 下載中心 」 下載的選擇性/重要。 累計更新可用 CU 知識庫文件中提供 Microsoft hotfix 的下載伺服器上。  
  
## <a name="see-also"></a>另請參閱  
 [從安裝精靈安裝 SQL Server 2014&#40;安裝程式&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [將功能加入至 SQL Server 2014 執行個體的&#40;安裝程式&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [卸除 SQL Server 2014 安裝](repair-a-failed-sql-server-installation.md)  
  
  
