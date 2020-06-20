---
title: Upgrade Advisor 必要條件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- requirements [Upgrade Advisor]
- software [Upgrade Advisor]
- system requirements [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, prerequisites
- prerequisites [Upgrade Advisor]
- Upgrade Advisor [SQL Server], prerequisites
ms.assetid: d21a39e5-5f81-4096-a7dd-f244e4779992
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 41c97cf585d1768c7aebeec2613ee8744cb220da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062357"
---
# <a name="upgrade-advisor-prerequisites"></a>Upgrade Advisor 必要條件
  此主題描述 Upgrade Advisor 的軟體需求。  
  
## <a name="prerequisites"></a>Prerequisites  
 安裝和執行 Upgrade Advisor 的必要條件如下：  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]SP1、[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] (從 SP2 開始)、Windows 7 或 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2。  
  
-   Windows Installer 4.5。 您可以從[Windows Installer 的網站](https://www.microsoft.com/download/details.aspx?id=8483)安裝 Windows Installer。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (從 .NET Framework 4 開始)。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 產品媒體上取得，並從 SDK、可轉散發套件[和 Service Pack 下載網站](https://go.microsoft.com/fwlink/?LinkId=48882)取得。  
  
    -   若要從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 媒體安裝 .NET Framework 4，請找出光碟機的根目錄。 接著按兩下 \redist 資料夾、按兩下 DotNetFrameworks 資料夾，然後執行 dotNetFx40_Full_x86_x64.exe (適用於 32 位元和 64 位元作業系統)。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安裝 upgrade advisor 的必要條件 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，而且不是由 Upgrade advisor 安裝程式所安裝。 安裝程式會要求您 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能套件下載並安裝 ScriptDom。  
  
## <a name="see-also"></a>另請參閱  
 [如何：安裝升級建議程式](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  
