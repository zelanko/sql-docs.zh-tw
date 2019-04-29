---
title: 步驟 1:建立新的 Integration Services 專案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2513a698fc073c751613e8e387d41ddb3e0fe9e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891757"
---
# <a name="step-1-creating-a-new-integration-services-project"></a>步驟 1:建立新的 Integration Services 專案
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立封裝的第一步就是建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 這個專案包含物件的範本 (資料來源、資料來源檢視和封裝)，您在資料轉換方案中會用到它們。  
  
 您在這個 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程中建立的封裝將解譯區分地區設定資料的值。 如果電腦未設定為使用地區設定選項 [英文 (美國)]，則您需要在封裝中設定其他屬性。 您在第 2 課到第 5 課使用的封裝，是從第 1 課建立的封裝複製而來，您不需要在複製的封裝中更新區分地區設定的屬性。  
  
> [!NOTE]  
>  這個教學課程需要 Microsoft SQL Server Data Tools。  
>   
>  如需有關安裝 SQL Server Data Tools 的詳細資訊，請參閱＜ [SQL Server Data Tools 下載](https://msdn.microsoft.com/data/hh297027)＞。  
  
### <a name="to-create-a-new-integration-services-project"></a>若要建立新的 Integration Services 專案  
  
1.  在 **[開始]** 功能表上，依序指向 **[所有程式]** 和 **[Microsoft SQL Server]**，然後按一下 **[SQL Server Data Tools]**。  
  
2.  在 **[檔案]** 功能表上，指向 **[新增]**，然後按一下 **[專案]** 來建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 **[新增專案]** 對話方塊中，展開 **[已安裝的範本]** 底下的 **[商業智慧]** 節點，然後選取 **[範本]** 窗格中的 **[Integration Services 專案]** 。  
  
4.  在 **[名稱]** 方塊中，將預設名稱變更為 **SSIS 教學課程**。 您可以選擇性地清除 **[建立方案的目錄]** 核取方塊。  
  
5.  接受預設位置，或按一下 **[瀏覽]** 來瀏覽並尋找您要使用的資料夾。 在 **[專案位置]** 對話方塊中，按一下該資料夾，然後按一下 **[選取資料夾]**。  
  
6.  按一下 [確定] 。  
  
     根據預設，系統會建立標題為 **Package.dtsx**的空白封裝，並加入至 SSIS 封裝底下的專案。  
  
7.  在 [ **方案總管** ] 工具列上，以滑鼠右鍵按一下 [ **Package.dtsx**]、按一下 **[重新命名]**，然後將預設封裝重新命名為 **Lesson 1.dtsx**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2：新增和設定一般檔案連線管理員](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
  
