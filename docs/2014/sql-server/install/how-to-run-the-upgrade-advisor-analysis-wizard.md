---
title: 如何： 執行 Upgrade Advisor 分析精靈 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5ff92f0bb0cbf15e61895307d799415639a89eab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136341"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>如何：執行 Upgrade Advisor 分析精靈
  您可以從 Upgrade Advisor 開始頁面啟動 Upgrade Advisor 分析精靈。 此主題描述如何執行 Upgrade Advisor 分析精靈。  
  
> [!IMPORTANT]  
>  執行 Upgrade Advisor 分析精靈時，Upgrade Advisor 會將報表儲存在預設報表資料夾中。 但是，報表檢視器只顯示最近儲存的五個報表。 報表的預設位置是我的文件\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports。  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>若要執行 Upgrade Advisor 分析精靈  
  
1.  在 Upgrade Advisor 開始頁面上，按一下 **啟動 Upgrade Advisor 分析精靈**。  
  
2.  在**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元件**頁面上，輸入要掃描中的伺服器名稱**伺服器名稱**方塊，然後再按一下**偵測**。 請按照下列伺服器名稱的指導方針進行：  
  
    -   若要掃描非叢集執行個體，請輸入電腦名稱。  
  
    -   若要掃描叢集執行個體，請輸入虛擬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱。  
  
    -   若要掃描安裝在叢集節點上的非叢集元件，請輸入節點名稱。  
  
    > [!WARNING]  
    >  Upgrade Advisor 不支援連接到未設定為使用標準通訊埠 (1433) 進行用戶端連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果要連接到不使用標準通訊埠 (1433) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，請使用 IP 位址和通訊埠建立別名。 如需設定用戶端通訊協定及建立別名的詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，請參閱[Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)。  
    >   
    >  如果您不需要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝在執行 Upgrade Advisor 的電腦上，按一下**啟動**，然後執行`cliconfg`。 這會開啟**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端網路公用程式** 對話方塊。 使用**別名**索引標籤來建立別名。  
  
3.  檢閱偵測到的元件清單，如有必要，修改選取範圍，然後按一下**下一步**。  
  
4.  在**連接參數**頁面上，選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您想要掃描、 選取驗證方法，如有必要，請輸入使用者名稱和密碼資訊，，，然後按一下**下一步**.  
  
     預設執行個體名稱是 MSSQLSERVER。  
  
5.  針對選取的元件，輸入要求的資訊。 如需有關個別對話方塊的詳細資訊，請參閱[Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)。  
  
6.  在**確認 Upgrade Advisor 設定**頁面上，檢閱您所輸入的資訊。 您可以選取**傳送報告給[!INCLUDE[msCoName](../../includes/msconame-md.md)]** 如果您想要提交升級報表。 您也可以檢閱隱私權原則。  
  
7.  按一下**執行**來分析執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
8.  當分析完成後時，按一下 **啟動報表**若要檢視偵測到的升級問題。  
  
## <a name="see-also"></a>另請參閱  
 [如何： 啟動 Upgrade Advisor](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [執行 Upgrade Advisor&#40;使用者介面&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  