---
title: 步驟 1:建立新的 Integration Services 專案 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 82420ce073f65483043d44670fc538849a447d90
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723321"
---
# <a name="lesson-1-1-create-a-new-integration-services-project"></a>第 1-1 課：建立新的 Integration Services 專案

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立封裝的第一步就是建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 這個範例專案包含資料來源、資料來源檢視和套件的範本，這些是構成資料轉換解決方案的要件。  
  
您在這個 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程中建立的套件會解譯區分地區設定資料的值。 如果電腦未設定為使用地區設定選項 [英文 (美國)]，您會需要在套件中設定其他屬性。 

您在第 2 課到第 6 課使用的套件，複製自您在這一課建立的套件。  
  
> [!NOTE]  
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。

## <a name="create-a-new-integration-services-project"></a>建立新的 Integration Services 專案  
  
1.  在 Windows 的 [開始] 功能表搜尋並選取 [Visual Studio (SSDT)]。  
  
2.  在 Visual Studio 中依序選取 [檔案] > [新增] > [專案] 以建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [新增專案] 對話方塊中，展開 [已安裝] 底下的 [商業智慧] 節點，然後選取 [範本] 窗格中的 [Integration Services 專案]。  
  
4.  在 **[名稱]** 方塊中，將預設名稱變更為 **SSIS 教學課程**。 若要使用已經存在的資料夾，請清除 [為解決方案建立目錄] 核取方塊。  
  
5.  接受預設位置，或選取 [瀏覽] 來瀏覽並尋找您要使用的資料夾。 在 [專案位置] 對話方塊中，依據選取該資料夾和 [選取資料夾]。  
  
6.  選取 [確定]。  
  
    根據預設，系統會建立標題為 **Package.dtsx** 的空白套件，並新增到您位在 [SSIS 套件] 下的專案。  
  
7.  在**方案總管**中，以滑鼠右鍵按一下 [Package.dtsx]，選取 [重新命名]，然後將預設套件重新命名為 **Lesson 1.dtsx**。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 2：新增及設定一般檔案連線管理員](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
