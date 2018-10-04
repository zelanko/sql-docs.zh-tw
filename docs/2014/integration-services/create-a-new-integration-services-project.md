---
title: 建立新的 Integration Services 專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Integration Services], creating
- Integration Services projects, creating
- SQL Server Integration Services projects, creating
- SSIS projects, creating
ms.assetid: 1e23f259-0401-4333-ab4f-89809aae63b1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4a571c48c0fa745d77c4d1def9a4e517376fad6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075658"
---
# <a name="create-a-new-integration-services-project"></a>建立新的 Integration Services 專案
  此程序會建立新的專案和新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 方案。  
  
### <a name="to-create-a-new-integration-services-project"></a>若要建立新的 Integration Services 專案  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]  
  
2.  在 **[檔案]** 功能表上，指向 **[開新檔案]**，然後按一下 **[專案]**。  
  
3.  在 **[新增專案]** 對話方塊的 **[範本]** 窗格中，選取 **[Integration Services 專案]** 範本。  
  
     **[Integration Services 專案]** 範本會建立一個包含單一、空白封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
4.  (選擇性) 編輯專案名稱和位置。  
  
     方案名稱會自動更新為符合專案名稱。  
  
5.  若要為方案檔建立個別的資料夾，請選取 **[為方案建立目錄]**。 這是預設選項。  
  
6.  如果電腦上安裝了原始檔控制軟體，請選取 **[加入至原始檔控制]**  以將專案與原始檔控制相關聯。  
  
7.  如果原始檔控制軟體是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe，則 **[Visual SourceSafe 登入]** 對話方塊會開啟。 請在 **[Visual SourceSafe 登入]** 中，提供使用者名稱、密碼，以及 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe 資料庫的名稱。 按一下 **[瀏覽]** 找出資料庫。  
  
    > [!NOTE]  
    >  若要檢視和變更選取的原始檔控制外掛程式，以及設定原始檔控制環境，請按一下 [工具] 功能表上的 [選項]，然後展開 [原始檔控制] 節點。  
  
8.  按一下  **確定**若要將方案加入**方案總管**r 及將專案加入方案。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;專案](integration-services-ssis-projects-and-solutions.md)   
 [在方案中新增或移除 Integration Services 專案](../../2014/integration-services/add-or-remove-an-integration-services-project-in-a-solution.md)  
  
  
