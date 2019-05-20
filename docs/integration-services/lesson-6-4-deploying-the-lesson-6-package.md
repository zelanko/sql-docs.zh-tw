---
title: 步驟 4：部署第 6 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4c843fa7af8e3390e820714886b7988edab878d
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65720817"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>第 6-4 課：部署第 6 課套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



部署套件時，需要將套件新增至 SQL Server 執行個體上 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的 SSISDB 目錄。 在本課程中，您會將第 6 課套件新增至 SSISDB 目錄、設定新的參數，並執行套件。 在本課程中，您會使用 SQL Server Management Studio 將第 6 課套件新增至 SSISDB 目錄，並部署套件。 部署套件之後，您可以修改參數以指向新位置，然後執行套件。   
在此工作中，您會：  

1. 將封裝加入至 SSISDB 目錄在 SQL Server 中的 [SSIS] 節點。  
  
2. 部署封裝。  
  
3. 設定封裝的參數值。  

4. 在 SSMS 中執行封裝。  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>尋找或新增 SSISDB 目錄  
  
1.  選取 [開始] > [所有程式] > [Microsoft SQL Server 2017]，然後選取 [SQL Management Studio]。  
  
2.  在 [連線到伺服器] 對話方塊上，確認預設值，然後選取 [連線]。 若要進行連線，**伺服器**名稱必須是 SQL Server 安裝所在電腦的名稱。 如果**資料庫引擎**是具名執行個體，則**伺服器**名稱必須是格式為 \<電腦名稱>\\\<執行個體名稱> 的執行個體名稱。 
  
3.  在 [物件總管] 中，展開 [Integration Services 目錄]。  
  
4.  如果 [Integration Services 目錄] 下未列出任何目錄，請新增 SSISDB 目錄。  
  
5.  若要新增 SSISDB 目錄，請以滑鼠右鍵按一下 [Integration Services 目錄]，然後選取 [建立目錄]。  
  
6.  在 [建立目錄] 對話方塊上，選取 [啟用 CLR 整合]。  
  
7.  在 [密碼] 方塊中輸入新密碼，然後在 [再次鍵入密碼] 方塊中再次輸入密碼。 
  
8.  選取 [確定] 以新增 SSISDB 目錄。  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>將套件新增至 SSISDB 目錄  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下 [SSISDB]，然後選取 [建立資料夾]。  
  
2.  在 [建立資料夾] 對話方塊的 [資料夾名稱] 方塊中，輸入 SSIS 教學課程，然後選取 [確定]。  
  
3.  展開 [SSIS 教學課程] 資料夾，以滑鼠右鍵按一下 [專案]，然後選取 [匯入套件]。  
  
4.  在 [Integration Services 專案轉換精靈] 的 [簡介] 頁面上，選取 [下一步]。  
  
5.  在 [尋找套件] 頁面上，確定已選取 [來源] 清單中的 [檔案系統]，然後選取 [瀏覽]。  
  
6.  在 [瀏覽資料夾] 對話方塊上，瀏覽至包含此 SSIS 教學課程專案的資料夾，然後選取 [確定]。  
  
7.  選取 **[下一步]**。  
  
8.  在 [選取套件] 頁面上，您應該會看到 SSIS 教學課程中的所有六個套件。 在 [套件] 清單中，選取 **Lesson 6.dtsx**，然後選取 [下一步]。  
  
9. 在 [選取目的地] 頁面的 [專案名稱] 方塊中，輸入 **SSIS 教學課程部署**，然後選取 [下一步]。

10. 在其餘每個精靈頁面上選取 [下一步]，直到到達 [檢閱] 頁面。  
  
11. 在 [檢閱] 頁面上，選取 [轉換]。  
  
12. 轉換完成之後，選取 [關閉]。  
  
當您關閉 Integration Services 專案轉換精靈時，SSIS 會顯示 Integration Services 部署精靈。 您現在可以使用此精靈來部署第 6 課套件。  
  
1.  在 [Integration Services 部署精靈] 的 [簡介] 頁面上，檢閱部署專案的步驟，然後選取 [下一步]。  
  
2.  在 [選取目的地] 頁面上，確認伺服器名稱是包含 SSISDB 目錄的 SQL Server 執行個體且路徑顯示 **SSIS 教學課程部署**，然後選取 [下一步]。  
  
3.  在 [檢閱] 頁面上檢閱 [摘要]，然後選取 [部署]。  
  
4.  部署完成時，選取 [關閉]。  
  
5.  在 [物件總管] 中，以滑鼠右鍵按一下 [Integration Services 目錄]，然後選取 [重新整理]。  
  
6.  展開 [Integration Services 目錄]，然後展開 [SSISDB]。 繼續展開 [SSIS 教學課程] 下的樹狀目錄，直到您已經完全展開專案。 您應該會在 [SSIS 教學課程部署] 節點的 [套件] 節點下，看到 **Lesson 6.dtsx**。  
  
7.  若要確認套件已完成，請以滑鼠右鍵按一下 **Lesson 6.dtsx**，然後選取 [設定]。 在 [設定] 對話方塊上，選取 [參數]，確認有一個以 **Lesson 6.dtsx** 為 [容器]、以 **VarFolderName** 為 [名稱] 並以**新範例資料**之路徑為值的項目，然後選取 [關閉]。  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>建立並填入新的範例資料夾  
  
1.  在 **Windows 檔案總管**中，於磁碟機的根目錄層級 (例如 **C:\\**) 建立一個名為 **Sample Data Two** 的資料夾。  
  
2.  開啟[第 1 課必要條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)中的 [Sample Data] 資料夾，然後複製任何三個範例檔案。  
  
3.  瀏覽至 [Sample Data Two] 資料夾並貼上複製的檔案。  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>變更套件參數以指向新的範例資料  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下 **Lesson 6.dtsx**，然後選取 [設定]。  
  
2.  在 [設定] 對話方塊上，將參數值變更為 **Sample Data Two** 的路徑，例如 **C:\\Sample Data Two**。  
  
3.  選取 [確定] 以關閉 [設定] 對話方塊。  
  
## <a name="test-the-lesson-6-package-deployment"></a>測試第 6 課套件部署  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下 **Lesson 6.dtsx**，然後選取 [執行]。  
  
2.  在 [執行套件] 對話方塊上，選取 [確定]。  
  
3.  在訊息對話方塊上，選取 [是] 以開啟 [概觀報表]。  
  
套件的 [概觀報表] 顯示套件的名稱和狀態摘要。 [執行概觀] 區段顯示套件中每個工作的結果。 [使用的參數] 區段顯示套件執行時所使用的所有參數名稱和值，包括 **VarFolderName**。  
  
