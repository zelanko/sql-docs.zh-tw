---
title: Upgrade Advisor 必要條件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d0ffd9ee070cbd0f5a00d560e5d1c5979d9ec52
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208540"
---
# <a name="upgrade-advisor-prerequisites"></a>Upgrade Advisor 必要條件
  此主題描述 Upgrade Advisor 的軟體需求。  
  
## <a name="prerequisites"></a>先決條件  
 安裝和執行 Upgrade Advisor 的必要條件如下：  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]SP1、[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] (從 SP2 開始)、Windows 7 或 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2。  
  
-   Windows Installer 4.5。 您可以安裝 Windows Installer 從[Windows Installer 網站](http://go.microsoft.com/fwlink/?LinkId=49112)。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (從 .NET Framework 4 開始)。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]位於[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]產品媒體，以及從[SDK、 可轉散發套件和 service pack 下載網站](http://go.microsoft.com/fwlink/?LinkId=48882)。  
  
    -   若要從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 媒體安裝 .NET Framework 4，請找出光碟機的根目錄。 接著按兩下 \redist 資料夾、按兩下 DotNetFrameworks 資料夾，然後執行 dotNetFx40_Full_x86_x64.exe (適用於 32 位元和 64 位元作業系統)。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 是安裝的必要條件[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Upgrade Advisor，並不會安裝 Upgrade Advisor 安裝程式。 安裝程式會要求您下載並安裝[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom 從[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Feature Pack。  
  
## <a name="see-also"></a>另請參閱  
 [如何：安裝升級建議程式](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  
