---
title: 連接至原生模式報表伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 5bf32c8427679b342bee89d6541b051beed2e8ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952293"
---
# <a name="connect-to-a-native-mode-report-server"></a>連接至原生模式報表伺服器
  使用此對話方塊可連接到本機或遠端 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器執行個體。 您無法使用此工具來連接到舊版的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器。 您一次只能連接到一個執行個體。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員不會用來設定及管理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。 您可以使用 SharePoint 管理中心和 PowerShell 指令碼，在 SharePoint 模式下設定報表伺服器。 如需詳細資訊，請參閱＜ [安裝適用於 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)＞  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager （rsconfigtool.exe）是以 "highestAvailable" 的許可權層級來安裝。 這是設計的行為。 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員需要與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API 進行通訊。 某些 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 通訊需要更高層級或系統管理權限。  
  
-   若要連接到本機報表伺服器執行個體，請使用預設值，然後按一下 **[連接]**。 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會提供本機伺服器名稱，並偵測預設執行個體。 在大部分情況下，您可以按一下 **[連接]** 而不必變更值。 如果您安裝了一個以上的執行個體，您必須選取您想要使用的執行個體。  
  
-   若要連接到遠端報表伺服器執行個體，請輸入伺服器名稱，再按一下 **[尋找]**，並選取此執行個體，然後按一下 **[連接]**。  
  
 若要開啟此對話方塊，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。 當您啟動此工具時，這個對話方塊會立即出現。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項。  
 **伺服器名稱**  
 輸入安裝 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之電腦的網路名稱。 只需要輸入電腦名稱；請勿包含前置詞或斜線。  
  
 **尋找**  
 尋找 **[伺服器名稱]** 中指定的電腦。  
  
 **報表伺服器執行個體**  
 如果安裝了多個報表伺服器執行個體，請選取要連接哪一個執行個體。 只有有效的執行個體可供選取。 如果您要將舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體並存執行，這些執行個體將不會出現在清單中。  
  
 **連線**  
 連接到您所指定的伺服器和執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
