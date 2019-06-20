---
title: HOW TO：安裝 Upgrade Advisor |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094915"
---
# <a name="how-to-install-upgrade-advisor"></a>HOW TO：安裝 Upgrade Advisor
  Upgrade Advisor 支援所有支援元件 ([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 除外) 的遠端分析。 如果您不要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的執行個體，可以將 Upgrade Advisor 安裝在可連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的任何電腦上。 電腦也必須符合 Upgrade Advisor 必要條件。 如果您要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的執行個體，則必須將 Upgrade Advisor 安裝在報表伺服器上。  
  
 如需詳細資訊，請參閱 < [Installing Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md)。  
  
### <a name="to-install-upgrade-advisor"></a>安裝 Upgrade Advisor  
  
1.  您可以使用下列其中一種方法來啟動安裝程序：  
  
    -   如果您從安裝[!INCLUDE[msCoName](../../includes/msconame-md.md)]網站時，請按一下 **下載**連結，然後按一下**執行**按鈕以開始安裝。  
  
    -   如果您要從產品媒體安裝，開啟**redist**資料夾中，開啟**Upgrade Advisor**資料夾，然後再按兩下**SQLUA.msi**。  
  
    > [!NOTE]  
    >  Upgrade Advisor 需要 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4。 如果您沒有安裝此元件，或者擁有發行前版本，系統就會顯示錯誤訊息。 請解除安裝任何舊版 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，然後安裝最新版 .NET Framework 4。  
    >   
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安裝的必要條件[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Upgrade Advisor，並不會安裝 Upgrade Advisor 安裝程式。 安裝程式會要求您下載並安裝[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 從[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Feature Pack。  
  
2.  在 [**歡迎[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Upgrade Advisor 安裝程式**頁面上，按一下**下一步]** 。  
  
3.  在 **授權合約**頁面上，閱讀授權合約。 如果您同意，請選取**我接受授權合約**，然後按一下**下一步**。  
  
4.  在 **註冊資訊**頁面上，輸入您的名稱和公司。  
  
5.  在 **特徵**頁面上，檢閱**安裝路徑**值。 如有必要，使用**瀏覽**按鈕來變更位置。 按一下 [下一步]  。  
  
6.  在上**安裝程式準備好**頁面上，按一下**安裝**以便安裝 Upgrade Advisor。  
  
7.  按一下 [完成]  結束精靈。  
  
## <a name="see-also"></a>另請參閱  
 [升級建議程式必要條件](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
