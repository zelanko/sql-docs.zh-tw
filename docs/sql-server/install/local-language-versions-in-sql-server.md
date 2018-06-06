---
title: SQL Server 中的地區語言版本 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5c91bea97846dfb5321eb514ad7993403aefa8a
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34772424"
---
# <a name="local-language-versions-in-sql-server"></a>SQL Server 中的地區語言版本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Windows 作業系統所支援的所有語言。  
  
## <a name="cross-language-support"></a>跨語言支援  
  
-   所有當地語系化版本的作業系統都支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的英文版。  
  
-   透過使用 Windows 多語系使用者介面 (MUI) 套件設定，便可在支援的作業系統對應語言版本或英文版的當地語系化作業系統上支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的當地語系化版本。 如需詳細資訊，請參閱 [Configure Operating System to Support Localized Versions](../../sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS)。  
  
-   當地語系化版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只能升級到相同語言的當地語系化版本，不能升級到英文版。  
  
-   當地語系化版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以與英文版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體並存安裝。  
  
##  <a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 透過使用 Windows 多語系使用者介面 (MUI) 套件設定， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的當地語系化版本可在支援的作業系統英文版上受到支援。  
  
 不過，在以非英文 MUI 設定執行英文版作業系統的伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的當地語系化版本之前，您必須確認某些作業系統設定。 您需要確認下列作業系統設定是否符合要安裝的當地語系化之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的語言：  
  
-   作業系統使用者介面設定  
  
-   作業系統使用者地區設定  
  
-   系統地區設定  
  
 如果設定不符合當地語系化之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的語言，請使用下列程序，正確設定這些作業系統設定。  
  
> [!CAUTION]  
>  不支援在相同電腦上安裝不同語言版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>若要變更作業系統使用者介面設定  
  
1.  如果尚未安裝，請安裝符合當地語系化版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的作業系統 MUI。  
  
2.  在 [控制台] 中，開啟 **[地區及語言選項]**。  
  
3.  在 **[語言]** 索引標籤上，針對 **[用於功能表和對話方塊的語言]**，從清單中選取一值。  
  
     這項設定將影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的使用者介面語言，因此它必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的當地語系化版本。  
  
4.  按一下 **[套用]** 來確認變更，並按一下 **[確定]** 來關閉視窗。  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>若要變更作業系統使用者地區設定  
  
1.  如果尚未安裝，請安裝符合當地語系化版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的作業系統 MUI。  
  
2.  在 [控制台] 中，開啟 **[地區及語言選項]**。  
  
3.  在 **[地區選項]** 索引標籤上，針對 **[選擇一個項目來符合它的喜好設定]**，從清單中選取一值。  
  
     這項設定會影響特定文化專用的資料格式。  
  
4.  按一下 **[套用]** 來確認變更，並按一下 **[確定]** 來關閉視窗。  
  
#### <a name="to-change-the-system-locale-setting"></a>若要變更系統地區設定  
  
1.  如果尚未安裝，請安裝符合當地語系化版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的作業系統 MUI。  
  
2.  在 [控制台] 中，開啟 **[地區及語言選項]**。  
  
3.  在 [進階] 索引標籤上，針對 [選擇一個符合於您要使用的非 Unicode 程式語言版本的語言]，從清單中選取一值。  
  
     這項設定可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝選擇最佳預設定序。  
  
4.  按一下 **[套用]** 來確認變更，並按一下 **[確定]** 來關閉視窗。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [安裝 SQL Server](../../database-engine/install-windows/install-sql-server.md)  
  
  
