---
title: "步驟 1：建立新的 Integration Services 專案 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8def799baa8e57c57bce0255894cf00325d68dfc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-1-1---creating-a-new-integration-services-project"></a>課程 1-1 - 建立新的 Integration Services 專案
在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中建立封裝的第一步就是建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 這個專案包含物件的範本 — 資料來源、資料來源檢視和封裝 — 您在資料轉換方案中會用到它們。  
  
您在這個 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程中建立的封裝將解譯區分地區設定資料的值。 如果電腦未設定為使用地區設定選項 [英文 (美國)]，則您需要在封裝中設定其他屬性。 您在第 2 課到第 5 課使用的封裝，是從第 1 課建立的封裝複製而來，您不需要在複製的封裝中更新區分地區設定的屬性。  
  
> [!NOTE]  
> 這個教學課程需要 Microsoft SQL Server Data Tools。  
>   
> 如需安裝 SQL Server Data Tools 的詳細資訊，請參閱 [SQL Server Data Tools 下載](http://msdn.microsoft.com/en-us/data/hh297027)。  
  
### <a name="to-create-a-new-integration-services-project"></a>若要建立新的 Integration Services 專案  
  
1.  在 **[開始]** 功能表上，依序指向 **[所有程式]**和 **[Microsoft SQL Server]**，然後按一下 **[SQL Server Data Tools]**。  
  
2.  在 **[檔案]** 功能表上，指向 **[新增]**，然後按一下 **[專案]** 來建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 **[新增專案]** 對話方塊中，展開 **[已安裝的範本]** 底下的 **[商業智慧]**節點，然後選取 **[範本]** 窗格中的 **[Integration Services 專案]** 。  
  
4.  在 **[名稱]** 方塊中，將預設名稱變更為 **SSIS 教學課程**。 您可以選擇性地清除 **[建立方案的目錄]** 核取方塊。  
  
5.  接受預設位置，或按一下 **[瀏覽]** 來瀏覽並尋找您要使用的資料夾。 在 **[專案位置]** 對話方塊中，按一下該資料夾，然後按一下 **[選取資料夾]**。  
  
6.  按一下 **[確定]**。  
  
    根據預設，系統會建立標題為 **Package.dtsx**的空白封裝，並加入至 SSIS 封裝底下的專案。  
  
7.  在 [ **方案總管** ] 工具列上，以滑鼠右鍵按一下 [ **Package.dtsx**]、按一下 **[重新命名]**，然後將預設封裝重新命名為 **Lesson 1.dtsx**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 2：加入和設定一般檔案連接管理員](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
