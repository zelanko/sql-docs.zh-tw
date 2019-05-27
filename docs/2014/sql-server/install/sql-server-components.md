---
title: SQL Server 元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 52045095714bfc2be7e929ed27a26a800c860fe6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092086"
---
# <a name="sql-server-components"></a>SQL Server 元件
  您可以針對已在本機或遠端電腦執行 Upgrade Advisor 分析精靈[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]安裝。 升級前分析的第一個步驟是識別要分析的電腦和元件。  
  
## <a name="options"></a>選項。  
 **電腦名稱**  
 指定要分析之電腦的名稱。 Upgrade Advisor 會填入**伺服器名稱**與本機電腦名稱 方塊中的。 您也可以使用 "." 和 "localhost" 來連接至本機電腦。  
  
 若要分析不同的電腦，請使用下列指導方針：  
  
-   若要掃描非叢集執行個體，請輸入電腦名稱。  
  
-   若要掃描叢集執行個體，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的名稱。  
  
-   若要掃描安裝在某個叢集之節點上的非叢集元件，請輸入容錯移轉叢集節點的電腦名稱。  
  
    > [!IMPORTANT]  
    >  請勿包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
 除了指定電腦名稱以外，您也可以指定 IP 位址。  
  
 若要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，您必須指定本機電腦的名稱。 Upgrade Advisor 只會掃描本機報表伺服器。  
  
 **偵測**  
 **偵測**按鈕存取指定的電腦，並偵測要分析的元件：  
  
-   如果要分析遠端電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，則必須在遠端電腦上啟用遠端登錄服務。  
  
-   如果在電腦的登錄中找到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 執行個體，就會偵測到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
-   如果在電腦的登錄中找到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，就會偵測出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
-   如果在電腦的登錄中找到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，就會偵測出 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 不過，Upgrade Advisor 只會掃描本機報表伺服器。  
  
 **Components**  
 選取要分析的元件。 您可以按一下**偵測** 按鈕以選取的電腦上安裝的所有元件。 偵測出安裝在電腦上的元件旁將顯示一個核取記號。 您也可以選取或清除每個元件旁的核取方塊，藉以手動選取要分析的元件。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
