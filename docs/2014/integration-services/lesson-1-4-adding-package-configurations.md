---
title: 步驟 4：新增套件設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 29da6dedad91566c0d111acfeb18b3778d2da4df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308118"
---
# <a name="step-4-adding-package-configurations"></a>步驟 4：加入封裝組態
  在這項工作中，您會為每個封裝加入組態。 組態會在執行階段更新封裝屬性和封裝物件的值。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供各種組態類型。 您可以將組態儲存在環境變數、登錄項目、使用者自訂變數、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表和 XML 檔案中。 為了提供更大的彈性， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 還支援使用間接組態。 這表示您可以使用環境變數來指定組態的位置，進而指定實際的值。 「部署教學課程」專案中的封裝會使用 XML 組態檔和間接組態的組合。 XML 組態檔可以包含多個屬性的組態，而且在適當的情況下，可以由多個封裝參考。 在這個教學課程中，您會針對各個封裝使用不同的組態檔。  
  
 組態檔通常會包含像是連接字串等機密資訊。 因此，您應該使用存取控制清單 (ACL) 來限制對儲存檔案所在位置或資料夾的存取，只將存取權授與給允許執行封裝的使用者或帳戶。 如需詳細資訊，請參閱[對封裝使用之檔案的存取權](../../2014/integration-services/access-to-files-used-by-packages.md)。  
  
 您在前一項工作中加入至「部署教學課程」專案的封裝 (DataTransfer 和 LoadXMLData) 需要設定，才能在部署到目標伺服器之後順利執行。 若要實作組態，必須先為 XML 組態檔建立間接組態，然後再建立 XML 組態檔。  
  
 您將會建立兩個組態檔 DataTransferConfig.dtsConfig 和 LoadXMLData.dtsConfig。 這些檔案包含了可更新封裝內屬性的名稱-值組，這些屬性會指定封裝所用之資料檔和記錄檔的位置。 在部署程序的稍後步驟中，您將會更新組態檔中的值，以反映這些檔案在目的地電腦上的新位置。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 知道 DataTransferConfig.dtsConfig 和 LoadXMLData.dtsConfig 是 DataTransfer 和 LoadXMLData 封裝的相依性，因此當您在下一課中建立部署配套時，將會自動包含組態檔。  
  
### <a name="to-create-indirect-configuration-for-the-datatransfer-package"></a>若要為 DataTransfer 封裝建立間接組態  
  
1.  在 [方案總管] 中，按兩下 DataTransfer.dtsx。  
  
2.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下控制流程設計介面背景中的任何位置。  
  
3.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
4.  在 [Package Configuration Organize (封裝組態組合管理)] 對話方塊中，選取 [啟用封裝組態] (如果尚未選取的話)，然後按一下 [加入]。  
  
5.  在 [封裝組態精靈] 的歡迎使用頁面上，按一下 [下一步]。  
  
6.  在 [選取組態類型] 頁面中，選取**XML 組態檔**中**組態類型**清單中，選取**組態位置儲存在環境變數**選項，然後輸入`DataTransfer,`或選取**DataTransfer**清單中的環境變數。  
  
    > [!NOTE]  
    >  若要在清單中提供環境變數，可能必須在加入變數之後重新啟動電腦。 如果不想要重新啟動電腦，可以輸入環境變數的名稱。  
  
7.  按 [下一步] 。  
  
8.  在 [正在完成精靈] 頁面的 [組態名稱] 方塊中，輸入「DataTransfer 環境變數組態」、在 [預覽] 窗格中檢閱組態內容，然後按一下 [完成]。  
  
9. 關閉 [Package Configuration Organize (封裝組態組合管理)] 對話方塊。  
  
### <a name="to-create-the-xml-configuration-for-the-datatransfer-package"></a>若要為 DataTransfer 封裝建立 XML 組態  
  
1.  在 [方案總管] 中，按兩下 DataTransfer.dtsx。  
  
2.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下控制流程設計介面背景中的任何位置。  
  
3.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
4.  在 [Package Configuration Organizer (封裝組態組合管理)] 對話方塊中，選取 [啟用封裝組態] 核取方塊，然後按一下 [加入]。  
  
5.  在 [封裝組態精靈] 的歡迎使用頁面上，按一下 [下一步]。  
  
6.  在 [選取組態類型] 頁面上，從 [組態類型] 清單中選取 [XML 組態檔]，然後按一下 [瀏覽]。  
  
7.  在 [選取組態檔位置] 對話方塊中，導覽至 C:\DeploymentTutorial 並且在 [檔案名稱] 方塊中輸入 **DataTransferConfig**，然後按一下 [儲存]。  
  
8.  在 [選取組態類型] 頁面上，按一下 [下一步]。  
  
9. 在 [選取要匯出的屬性] 頁面上，依序展開 [DataTransfer]、[連接管理員]、[Deployment Tutorial Log] 和 [屬性]，然後選取 [連接字串] 核取方塊。  
  
10. 在 [連接管理員] 內，展開 [NewCustomers]，然後選取 [連接字串] 核取方塊。  
  
11. 按 [下一步] 。  
  
12. 在 [正在完成精靈] 頁面的 [組態名稱] 方塊中，輸入「DataTransfer 組態」、檢閱組態的內容，然後按一下 [完成]。  
  
13. 在 [Package Configuration Organizer (封裝組態組合管理)] 對話方塊中，確認第一個列出的是「DataTransfer 環境變數組態」，第二個列出的是「DataTransfer 組態」，然後按一下 [關閉]。  
  
### <a name="to-create-indirect-configuration-for-the-loadxmldata-package"></a>若要為 LoadXMLData 封裝建立間接組態  
  
1.  在 [方案總管] 中，按兩下 LoadXMLData.dtsx。  
  
2.  在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下控制流程設計介面背景中的任何位置。  
  
3.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
4.  在 [Package Configuration Organize (封裝組態組合管理)] 對話方塊中，按一下 [加入]。  
  
5.  在 [封裝組態精靈] 的歡迎使用頁面上，按一下 [下一步]。  
  
6.  在 [選取組態類型] 頁面中，選取**XML 組態檔**中**組態類型**清單中，選取**組態位置儲存在環境變數**選項，然後輸入`LoadXMLData`或選取`LoadXMLData`清單中的環境變數。  
  
    > [!NOTE]  
    >  若要在清單中提供環境變數，可能必須在加入變數之後重新啟動電腦。  
  
7.  按 [下一步] 。  
  
8.  在 [正在完成精靈] 頁面的 [組態名稱] 方塊中，輸入「LoadXMLData EV 組態」、檢閱組態的內容，然後按一下 [完成]。  
  
### <a name="to-create-the-xml-configuration-for-the-loadxmldata-package"></a>若要為 LoadXMLData 封裝建立 XML 組態  
  
1.  在 [方案總管] 中，按兩下 LoadXMLData.dtsx。  
  
2.  在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下控制流程設計介面背景中的任何位置。  
  
3.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
4.  在 [Package Configuration Organizer (封裝組態組合管理)] 對話方塊中，選取 [啟用封裝組態] 核取方塊，然後按一下 [加入]。  
  
5.  在 [封裝組態精靈] 的歡迎使用頁面上，按一下 [下一步]。  
  
6.  在 [選取組態類型] 頁面上，從 [組態類型] 清單中選取 [XML 組態檔]，然後按一下 [瀏覽]。  
  
7.  在 [選取組態檔位置] 對話方塊中，導覽至 C:\DeploymentTutorial 並且在 [檔案名稱] 方塊中輸入 **LoadXMLDataConfig**，然後按一下 [儲存]。  
  
8.  在 [選取組態類型] 頁面上，按一下 [下一步]。  
  
9. 在 [選取要匯出的屬性] 頁面上，依序展開 [LoadXMLData]、[可執行檔]、[載入 XML 資料] 和 [屬性]，然後選取 [[XMLSource].[XMLData]] 和 [[XMLSource].[XMLSchemaDefinition]] 核取方塊。  
  
10. 按 [下一步] 。  
  
11. 在 [正在完成精靈] 頁面的 [組態名稱] 方塊中，輸入「LoadXMLData 組態」、檢閱組態的內容，然後按一下 [完成]。  
  
12. 在 [Package Configuration Organizer (封裝組態組合管理)] 對話方塊中，確認第一個列出的是「LoadXMLData 環境變數組態」，第二個列出的是「LoadXMLData 組態」，然後按一下 [關閉]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 5：測試更新的套件](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期  **<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [封裝組態](../../2014/integration-services/package-configurations.md)   
 [建立封裝組態](../../2014/integration-services/create-package-configurations.md)   
 [套件所用檔案的存取](../../2014/integration-services/access-to-files-used-by-packages.md)  
  
  
