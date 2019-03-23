---
title: 步驟 2：建立部署專案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f5b0cc2c86ef483a7e2b2c0f5dccba21383641f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376636"
---
# <a name="step-2-creating-the-deployment-project"></a>步驟 2：建立部署專案
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中，可部署的單位是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。 部署封裝之前，必須先建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，並且將所有封裝以及要隨同封裝一起部署的所有輔助檔案全部加入至該專案中。  
  
### <a name="to-create-the-integration-services-project"></a>若要建立 Integration Services 專案  
  
1.  按一下 [開始]，依序指向 [所有程式] 和 [Microsoft SQL Server]，然後按一下 [SQL Server]、[SQL Server Data Tools]。  
  
2.  在 [檔案] 功能表上，指向 [開新檔案]，然後按一下 [專案] 建立新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [新增專案] 對話方塊中，選取 [範本] 窗格中的 [Integration Services 專案]。  
  
4.  在 [名稱] 方塊中，將預設名稱變更為**部署教學課程**。 您可以選擇性地清除 **[建立方案的目錄]** 核取方塊。  
  
5.  接受預設位置，或按一下 [瀏覽] 尋找您要使用的資料夾。  
  
6.  在 [專案位置] 對話方塊中，按一下該資料夾，然後按一下 [開啟]。  
  
7.  按一下 [確定] 。  
  
8.  依預設，會建立名稱為 Package.dtsx 的空白封裝，並將其加入至專案中。 但是，您並不會使用此封裝，而是將現有的封裝加入至專案中。 由於專案中的所有封裝都會包含在部署中，因此應該刪除 Package.dtsx。 若要刪除，請以滑鼠右鍵按一下這個檔案，然後按一下 [刪除]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 3：加入封裝和其他檔案](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 專案](integration-services-ssis-projects-and-solutions.md)  
  
  
