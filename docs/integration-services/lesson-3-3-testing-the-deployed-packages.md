---
title: 步驟 3：測試已部署的套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9159da3f-c9ca-4015-9e85-3bf4373a1349
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 697bc007072642209979347b2404adfa4e850b62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121494"
---
# <a name="lesson-3-3---testing-the-deployed-packages"></a>課程 3-3 - 測試已部署的套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


在這項工作中，您會測試已部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的封裝。  
  
在其他 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程中，則是使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)][偵錯] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]功能表上的 **[開始偵錯]** 選項，在 **(** 的開發環境) 中執行封裝。 這時將會以不同的方式執行封裝。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供了幾項工具，您可以用來在測試和實際執行環境中執行套件，這些工具為：命令提示字元公用程式 **dtexec** 和「執行套件公用程式」。 「執行封裝公用程式」是以 **dtexec**為基礎所建立的圖形化工具。 這兩項工具都會立即執行封裝。 此外， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 還提供了 SQL Server Agent 的子系統，這套子系統是特別設計的，它會將封裝執行排程為 SQL Server Agent 作業中的一個步驟。  
  
您將會使用「執行封裝公用程式」來執行部署的封裝。 封裝將會直接使用，因此，您不必更新對話方塊中任何頁面上的資訊。 您將會從 [一般] 頁面開始執行封裝，這也就是「執行封裝公用程式」的第一個頁面。 如果需要，可以按一下其他頁面，以查看頁面中所包含的各封裝資訊。  
  
> [!NOTE]  
> 為了確保封裝能夠在這個教學課程的內容中順利執行，請不要修改任何選項。  
  
使用「執行封裝公用程式」在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中執行封裝之前，請確定 Integration Services 服務正在執行中。 Integration Services 服務可提供封裝儲存體和執行的支援。 如果停止服務，就無法連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，而且 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 不會列出要執行的封裝。 此外，您還必須具有在部署封裝的執行個體上執行封裝的權限。 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../integration-services/security/integration-services-roles-ssis-service.md)。  
  
[存放的封裝] 資料夾內的最上層資料夾是使用者定義的資料夾，Integration Services 服務會加以監視。 您可以依照需要，在 MsDtsSrvr.ini.xml 檔案中指定任意個資料夾。 這個教學課程會假設您要使用預設的 MsDtsSrvr.ini.xml 檔案，而且 [存放的封裝] 資料夾內最上層資料夾的名稱分別為 File System 和 MSDB。  
  
### <a name="to-connect-to-integration-services-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中連接到 Integration Services  
  
1.  按一下 **[開始]** ，依序指向 **[所有程式]** 和 **[Microsoft SQL Server]** ，然後按一下 **[SQL Server Management Studio]** 。  
  
2.  在 **[連接到伺服器]** 對話方塊中，從 **[伺服器類型]** 清單中選取 **[Integration Services]** ，並在 **[伺服器名稱]** 方塊中提供伺服器名稱，然後按一下 **[連接]** 。  
  
    > [!IMPORTANT]  
    > 如果您無法連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務目前可能沒有執行。 若要了解此服務的狀態，請按一下 **[開始]** ，依序指向 **[所有程式]** 、 **[Microsoft SQL Server]** 和 **[組態工具]** ，然後按一下 **[SQL Server 組態管理員]** 。 在左窗格中，按一下 **[SQL Server 服務]** 。 在右窗格中，尋找 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 如果此服務尚未執行，請將它啟動。  
  
    [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 隨即開啟。 依預設，[物件總管] 視窗會開啟並放置在 SQL Server Management Studio 的右上角。 如果 [物件總管] 未開啟，請按一下 **[檢視]** 功能表上的 **[物件總管]** 。  
  
### <a name="to-run-the-packages-using-the-execute-package-utility"></a>若要使用執行封裝公用程式來執行封裝  
  
1.  在 [物件總管] 中，展開 [存放的封裝] 資料夾。  
  
2.  展開 [MSDB] 資料夾。 由於您已將封裝部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，因此所有部署的封裝都會存放在 msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中，而且所有部署的封裝都會出現在 MSDB 資料夾中。 除非您已將封裝部署到「部署教學課程」以外的檔案系統中，否則 [File System] 資料夾應該是空的。  
  
3.  從封裝清單的最上方開始，以滑鼠右鍵按一下 [DataTransfer]，然後按一下 **[執行封裝]** 。  
  
4.  在 **[執行封裝公用程式]** 對話方塊中，按一下 **[執行]** 。  
  
5.  在 **[執行封裝公用程式]** 對話方塊中，檢視封裝的執行進度和執行結果。 當 **[停止]** 按鈕變成無法使用的狀態時，即表示封裝已完成，請按一下 **[關閉]** 。  
  
    > [!IMPORTANT]  
    > 如果在封裝執行中按一下 **[停止]** ，封裝將無法完成。  
  
6.  在 **[執行封裝公用程式]** 對話方塊中，按一下 **[關閉]** 。  
  
7.  針對 LoadXML 封裝，重複步驟 3 到 6。  
  
8.  在 **[檔案]** 功能表上按一下 **[結束]** 。  
  
### <a name="to-verify-the-results-of-the-datatransfer-package"></a>若要確認 DataTransfer 封裝的結果  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的工具列上，按一下 **[新增查詢]** 。  
  
2.  在 **[連接到伺服器]** 對話方塊中，從 **[伺服器類型]** 清單中選取 **[Database Engine]** ，並在 **[伺服器名稱]** 方塊中提供安裝教學課程封裝所在的伺服器名稱或是輸入 (local)，然後選取驗證模式。 如果要使用「SQL Server 驗證」，請提供使用者名稱和密碼。  
  
3.  按一下 **[連接]** 。  
  
4.  在查詢視窗中，輸入或貼上下列 SQL 陳述式：  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM HighIncomeCustomers`  
  
5.  按 **F5** ，或按一下工具列上的 [執行] 圖示。  
  
    查詢會傳回 31 個資料列。 傳回結果包含文字檔 Customers.txt 中 [YearlyIncome] 資料行值大於 100000 的所有資料列。  
  
6.  找到 [DeploymentTutorial] 資料夾，以滑鼠右鍵按一下 XML 記錄檔 Deployment Tutorial Log，然後按一下 [開啟]  。 您可以使用「記事本」或其他文字/XML 編輯器來開啟此檔案。  
  
### <a name="to-verify-the-results-of-the-loadxmldata-package"></a>若要確認 LoadXMLData 封裝的結果  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的工具列上，按一下 **[新增查詢]** 。  
  
2.  如果提示您重新連接，請在 **[連接到伺服器]** 對話方塊中，從 **[伺服器類型]** 清單中選取 **[Database Engine]** ，並在 **[伺服器名稱]** 方塊中提供安裝教學課程封裝所在的伺服器名稱或是輸入 (local)，然後選取驗證模式。 如果要使用「SQL Server 驗證」，請提供使用者名稱和密碼。  
  
3.  按一下 **[連接]** 。  
  
4.  在查詢視窗中，輸入或貼上下列 SQL 陳述式：  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM OrderDatesByCountryRegion`  
  
5.  按 **F5** ，或按一下工具列上的 [執行] 圖示。  
  
    查詢會傳回 21 個資料列。 傳回結果是由 XML 資料檔 (orders.xml) 中的資料列所組成。 每一個資料列都是依國家/地區排序的摘要；資料列中會列出國家/地區的名稱、每個國家/地區的訂單數目，以及最新和最舊訂單的日期。  
  
## <a name="see-also"></a>另請參閱  
[dtexec 公用程式](../integration-services/packages/dtexec-utility.md)  
  
  
  
