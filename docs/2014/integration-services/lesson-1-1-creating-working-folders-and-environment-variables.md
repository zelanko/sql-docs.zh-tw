---
title: 步驟 1:建立工作資料夾與環境變數 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b58da11d973d169a0372e59c7e8d7e174e3cf789
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767650"
---
# <a name="step-1-creating-working-folders-and-environment-variables"></a>步驟 1:建立工作資料夾和環境變數
  在這項工作中，您將建立工作資料夾 (C:\DeploymentTutorial) 和新的系統環境變數 (`DataTransfer` 與 `LoadXMLData`)，並稍後在教學課程工作中使用。  
  
 工作資料夾位於 C 磁碟的根目錄。 如果必須使用其他磁碟或位置，這是可行的。 不過必須記下這個位置，只要教學課程提到 DeploymentTutorial 工作資料夾時就會用到這個位置。  
  
 在後面的課程中，您會將儲存在檔案系統中的套件部署到 msdb[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中的 sysssispackages 資料表。 理想的狀況是將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝部署到其他電腦。 如果不可行，但透過將封裝部署到本機電腦上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，您仍可從進行本課中學到許多知識。 本機電腦和目的電腦中使用的環境變數有著相同的名稱，但儲存在變數中的值則不同。 例如，本機電腦上環境變數 `DataTransfer` 的值會參考 C:\DeploymentTutorial 資料夾，而目標電腦上環境變數 `DataTransfer` 卻會參考 C:\DeploymentTutorialInstall 資料夾。  
  
 如果您打算部署到本機電腦，必須只建立一組環境變數，但在進行本機部署之前必須先將環境變數的值更新為適合的值。  
  
 如果您打算將封裝部署到其他電腦，必須建立兩組環境變數：一組用於本機電腦，另一組用於目的電腦。 您現在就可以先為來源電腦建立一個變數，而稍後再為目的電腦建立變數，但必須在目的電腦上有可用的資料夾和環境變數，才能安裝封裝。  
  
### <a name="to-create-the-local-working-folder"></a>建立本機工作資料夾  
  
1.  以滑鼠右鍵按一下 [開始] 功能表，然後按一下 [檔案總管]。  
  
2.  按一下 [本機磁碟 (C:)]。  
  
3.  在 [檔案] 功能表上，指向 [新增]，然後按一下 [資料夾]。  
  
4.  重新命名新的資料夾來`DeploymentTutorial`。  
  
### <a name="to-create-local-environment-variables"></a>建立基本環境變數  
  
1.  在 **[開始]** 功能表上，按一下 **[控制台]**。  
  
2.  在 [控制台] 中，按兩下 [系統]。  
  
3.  在 [系統內容] 對話方塊中，按一下 [進階] 索引標籤，然後按一下 [環境變數]。  
  
4.  在 [環境變數] 對話方塊的 [系統變數] 框架中，按一下 [新增]。  
  
5.  在**新增系統變數** 對話方塊中，輸入`DataTransfer`中**變數的名稱** 方塊中，並`C:\DeploymentTutorial\datatransferconfig.dtsconfig`中**變數值** 方塊中。  
  
6.  按一下 [確定] 。  
  
7.  按一下 **新增**同樣地，並輸入`LoadXMLData`中**變數名稱** 方塊中，和`C:\DeploymentTutorial\loadxmldataconfig.dtsconfig`中**變數值** 方塊中。  
  
8.  按一下 [確定]，結束 [環境變數] 對話方塊。  
  
9. 按一下 [確定]，結束 [系統內容] 對話方塊。  
  
10. 選擇性重新啟動電腦。 如果不重新啟動電腦，新的變數名稱不會在「封裝組態精靈」中顯示，但您仍然可以使用這個名稱。  
  
### <a name="to-create-destination-environment-variables"></a>建立目的環境變數  
  
1.  在 **[開始]** 功能表上，按一下 **[控制台]**。  
  
2.  在 [控制台] 中，按兩下 [系統]。  
  
3.  在 [系統內容] 對話方塊中，按一下 [進階] 索引標籤，然後按一下 [環境變數]。  
  
4.  在 [環境變數] 對話方塊的 [系統變數] 框架中，按一下 [新增]。  
  
5.  在**新的系統變數** 對話方塊中，輸入`DataTransfer`中**變數的名稱** 方塊中，和`C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig`中**變數值** 方塊中。  
  
6.  按一下 [確定] 。  
  
7.  按一下 **新增**同樣地，並輸入`LoadXMLData`中**變數名稱** 方塊中，和`C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig`中**變數值** 方塊中。  
  
8.  按一下 [確定]，結束 [環境變數] 對話方塊。  
  
9. 按一下 [確定]，結束 [系統內容] 對話方塊。  
  
10. 選擇性重新啟動電腦。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2：建立部署專案](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
