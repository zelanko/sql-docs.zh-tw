---
title: "步驟 4： 部署第 6 課封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 504d9be296088cf3f455f8790ff013ab0c1df14b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-6-4---deploying-the-lesson-6-package"></a>課程 6-4-第 6 課封裝部署
部署封裝時，需要將封裝新增至 SSISDB 目錄中的 SQL Server 執行個體上的整合服務。 在本課程中您會將第 6 課封裝加入至 SSISDB 目錄、 設定參數，以及執行封裝。 本課程中引導您使用 SQL Server Management Studio 來將第 6 課封裝加入至 SSISDB 目錄，以及部署封裝。 在部署封裝之後，您將修改參數指向新位置，然後執行封裝。  
  
在這一課中，您將會：  
  
-   將封裝加入至 SSISDB 目錄在 SQL Server 中的 [SSIS] 節點。  
  
-   部署封裝。  
  
-   設定封裝的參數值。  
  
-   在 SSMS 中執行封裝。  
  
### <a name="to-locate-or-add-the-the-ssisdb-catalog"></a>若要尋找或加入 SSISDB 目錄  
  
1.  按一下 [開始]，指向 [所有程式]、 指向 Microsoft SQL Server 2012，，然後按一下 [SQL Management Studio]。  
  
2.  在 [連接到伺服器] 對話方塊中，驗證預設值，再按一下 [連接]。 若要連接，[伺服器名稱] 方塊必須包含已安裝 SQL Server 的電腦名稱。 如果資料庫引擎是具名執行個體，[伺服器名稱] 方塊也應該包含執行個體名稱，其格式為 <電腦名稱>\\<執行個體名稱>。  
  
3.  在 [物件總管] 中展開 [Integration Services 目錄]。  
  
4.  如果沒有列在 [Integration Services 目錄] 下的目錄則新增 SSISDB 目錄。  
  
5.  若要新增 SSISDB 目錄，以滑鼠右鍵按一下 [Integration Services 目錄]，並按一下 [建立類別目錄]。  
  
6.  在 [建立類別目錄] 對話方塊中選取 [啟用 CLR 整合]。  
  
7.  在 [密碼] 方塊中，輸入新密碼，然後在 [重新輸入密碼] 方塊中再次輸入。 請務必記得您輸入的密碼。  
  
8.  按一下 [確定] 以新增 SSISDB 目錄。  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>若要將封裝加入至 SSISDB 目錄  
  
1.  在 [物件總管] 中以滑鼠右鍵按一下 [SSISDB] 並按一下 [建立資料夾]。  
  
2.  在 [建立資料夾] 對話方塊中，請在 [資料夾名稱] 方塊中輸入 SSIS 教學課程，然後按一下 [確定]。  
  
3.  展開 [SSIS 教學課程] 資料夾、 以滑鼠右鍵按一下專案，再按一下 [匯入套件]。  
  
4.  在 [Integration Services 專案轉換精靈簡介] 頁面上按一下 [下一步]。  
  
5.  在 [尋找封裝] 頁面中，確定已選取 [來源] 清單中的 [檔案] 系統，然後按一下 [瀏覽]。  
  
6.  在 [瀏覽資料夾] 對話方塊中，瀏覽至包含 SSIS 教學課程專案的資料夾，然後按一下 [確定]。  
  
7.  按 [下一步]。  
  
8.  在 [選取封裝] 頁面上，您應該看到從 SSIS 教學課程的所有六個封裝。 在封裝清單中，選取 [Lesson 6.dtsx]，然後按一下 [下一步]。  
  
9. 在 [選取目的地] 頁面中，在 [專案名稱] 方塊中輸入 SSIS 教學課程部署，然後按一下 [下一步]。  
  
10. 接下來在每個其餘的精靈頁面上按一下 [下一步] 直到到達 [檢閱] 頁面。  
  
11. 在 [檢閱] 頁面中，按一下 [轉換]。  
  
12. 轉換完成時，請按一下 [關閉]。  
  
當您關閉 Integration Services 專案轉換精靈時，SSIS 會顯示 Integration Services 部署精靈。 現在您將使用此精靈部署第 6 課封裝。  
  
1.  在 [Integration Services 部署精靈簡介] 頁面中，檢閱部署專案的步驟，然後按一下 [下一步]。  
  
2.  在 [選取目的地] 頁面上確認伺服器名稱是包含 SSISDB 目錄的 SQL Server 執行個體和路徑顯示 SSIS 教學課程部署，然後按一下 [下一步]。  
  
3.  在 [檢閱] 頁面上檢閱摘要，然後按一下 [部署]。  
  
4.  部署完成時，請按一下 [關閉]。  
  
5.  在 [物件總管] 中以滑鼠右鍵按一下 [Integration Services 目錄]，並按一下 [重新整理]。  
  
6.  依序展開 Integration Services 目錄 SSISDB。 繼續展開下 SSIS 教學課程的樹狀目錄，直到您已經完全展開專案。 您應該會看到 [SSIS 教學課程部署] 節點的 [封裝] 節點下的 Lesson 6.dtsx。  
  
若要確認封裝已完成，以滑鼠右鍵按一下 Lesson 6.dtsx 並按一下 [設定]。 在 [設定] 對話方塊中，選取參數並確認有作為容器的 Lesson 6.dtsx 項目、作為名稱的 VarFolderName 及作為值的新範例資料的路徑，然後按一下 [關閉]。  
  
繼續建立新的範例資料資料夾之前，命名為 [範例資料兩個]，並將任何三個原始範例檔案複製到其中。  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>若要建立及擴展新的範例資料夾  
  
1.  在 Windows 檔案總管中，於磁碟機的根目錄層級 (例如 C:\\) 建立一個稱為 Sample Data Two 的新資料夾。  
  
2.  開啟 c:\Program Files\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data 資料夾，然後從資料夾複製三個範例檔案。  
  
3.  在新範例資料資料夾，貼上已複製的檔案。  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>若要變更為指向新的範例資料的封裝參數  
  
1.  在 [物件總管] 中以滑鼠右鍵按一下 Lesson 6.dtsx 並按一下 [設定]。  
  
2.  在 [設定] 對話方塊中，變更參數值為 [範例資料兩個] 的路徑。 例如 C:\範例資料兩個，如果您在 C 磁碟機上的根資料夾中放置新的資料夾。  
  
3.  按一下 [確定] 關閉 [設定] 對話方塊。  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>若要測試第 6 課封裝部署  
  
1.  在 [物件總管] 中以滑鼠右鍵按一下 Lesson 6.dtsx 並按一下 [執行]。  
  
2.  在 [執行封裝] 對話方塊中，按一下 [確定]。  
  
3.  在訊息對話方塊中按一下 [是] 以開啟概觀報表。  
  
概觀報表中的封裝便會顯示名稱的封裝和狀態摘要。 [執行概觀] 一節顯示封裝中的每個工作的結果，而 [使用參數] 一節顯示封裝中所有使用參數的名稱和值，包括 VarFolderName 所用的所有參數。  
  
  
  

