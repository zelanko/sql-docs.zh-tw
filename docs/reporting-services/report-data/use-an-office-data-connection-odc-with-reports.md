---
title: "搭配報表使用 Office 資料連線 (.odc) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7df29304e469a78f64a8b81198d7991f956953fe
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="use-an-office-data-connection-odc-with-reports"></a>搭配報表使用 Office 資料連線 (.odc)
  在少數情況下，您可以使用現有的 Office 資料連線 (.odc) 檔案來提供連接資訊給 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。 建立共用資料來源時，您可以使用 .odc 檔案來取代 .rsds 檔案。 報表伺服器使用 .odc 檔案的方式與使用 .rsds 檔案相同。報表伺服器會讀取檔案，找出資料來源類型、連接字串和認證資訊。  
  
 並非所有 .odc 檔案都可用於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。 .odc 可用與否取決於資料處理延伸模組以及報表和 .odc 檔案的特性：  
  
-   報表必須設計成可以使用 OLE DB 或 ODBC 資料提供者。 如果您使用不同的資料處理延伸模組建立報表，則報表及其查詢可能會包含 OLE DB 或 ODBC 資料提供者不支援的功能。  
  
-   .odc 檔案必須擁有必要的元素和結構。 檔案中必須明確設定資料提供者和認證設定，以供報表伺服器讀取。 設定這些值的最佳方式是先匯出 .odc 檔案，再將檔案上傳到 SharePoint 程式庫。  
  
-   .odc 檔案必須指定 OLE DB 或 ODBC 連接類型。  
  
-   .odc 檔案必須指定連接字串。  
  
-   認證可以設為 [無]、[預存] 或 [整合式]。 如果認證方法設定為 [預存]，報表伺服器將會提示使用者輸入認證，而不會使用預存認證。 報表伺服器無法依照 .odc 檔案的定義使用預存認證。  
  
-   資料來源擁有的結構描述必須與用來建立報表的結構描述相同。 如果資料結構不同，報表便無法執行。  
  
-   您必須在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007 (舊版 .odc 與報表定義檔不相容) 中建立此 .odc 檔案。  
  
 即使 .odc 資料來源類型看起來和支援的資料來源類型非常相似，您使用的 .odc 檔案也不能指定無法在報表伺服器上處理之資料來源的連接。 具體而言，如果您在 Microsoft Excel 2007 中建立了從 Microsoft Access、網路或文字檔擷取資料的 .odc 檔案，便無法使用該 .odc 檔案來提供資料給報表。  
  
 報表產生器報表及模型無法使用 .odc 檔案。 您不能使用 .odc 檔案產生模型，也不能將模型設定為使用連結到 .odc 檔案的共用資料來源。  
  
 如果您不熟悉 .odc 檔案，可以依照下列指示來建立及匯出檔案。 為 OLE DB 資料來源建立 .odc 檔案的簡單方式為使用 Excel 2007 和資料連線精靈。 但請注意，這個精靈並不會建立資料來源，您必須擁有已經定義的外部資料來源。  
  
 現有的 .odc 檔案必須與報表與查詢完全相容，您才能使用該檔案。 如果發生需要大幅修改報表或 .odc 檔案的錯誤，則應為報表建立新的 .rsds 檔案。 如需如何建立使用 .rsds 檔案之共用資料來源的詳細資訊，請參閱[建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)。  
  
### <a name="to-create-and-export-an-odc-file"></a>建立及匯出 .odc 檔案  
  
1.  啟動 Excel 2007。  
  
2.  在 [資料] 索引標籤的 [取得外部資料] 群組中，按一下 [從其他來源]，然後按一下 [從資料連線精靈]。  
  
3.  選取 [其他/進階]，然後按 [下一步]。  
  
4.  選取 [Microsoft OLE DB Provider for SQL Server]，然後按 [下一步]。  
  
5.  輸入伺服器的名稱 (根據預設，此名稱為電腦的網路名稱) 以及具備有效登入和資料庫權限的使用者帳戶。 按一下 **[下一步]**。  
  
6.  選取資料庫，然後按一下 [確定] 關閉 [資料連結] 對話方塊。  
  
7.  [連接至特定資料表] 核取方塊為預設選取項目， 並且用來結取特定資料表中的資料。 報表伺服器會忽略 .odc 檔案中的所有查詢，因此不論您選取或清除這個核取方塊都不會有影響。 為報表擷取資料的查詢會包含在報表定義檔案中，而非外部檔案中。  
  
8.  當連線開啟時，您可以編輯屬性並將它匯出。 請在 [資料] 索引標籤的 [連線] 群組中，按一下 [屬性]，然後按一下連接名稱旁的 [連線屬性] 按鈕。  
  
9. 在 [定義] 索引標籤上，按一下[匯出連線檔案]。  
  
10. 輸入檔案名稱，然後按一下 [儲存]。 接著關閉應用程式和所有已開啟的檔案。  
  
### <a name="to-upload-and-use-an-odc-file"></a>上傳及使用 .odc 檔案  
  
1.  開啟您要上傳連接檔案的目標文件庫。  
  
2.  在 [上傳] 功能表上，按一下 [上傳文件]。  
  
3.  按一下 **[瀏覽]**。  
  
4.  選取您建立的 .odc 檔案。 依預設，.odc 檔案位於 [我的文件] 資料夾的 [我的資料來源] 中。  
  
5.  按一下 [開啟] 選取檔案，然後按一下 [確定] 儲存所選項目。 新項目的屬性頁會自動開啟。  
  
6.  在 [內容類型] 中，選取 [報表資料來源]，然後按一下 [確定]。  
  
7.  指向報表。  
  
8.  按一下向下箭頭，然後選取 [管理資料來源]。  
  
9. 按一下資料來源名稱。  
  
10. 如果報表使用自訂資料來源資訊，請按一下 [共用]。  
  
11. 在 [資料來源連結] 中，按一下瀏覽 (**...**) 按鈕。  
  
12. 選取剛才上傳的 .odc 檔案。  
  
13. 按一下 [確定] 選取檔案，然後按一下 [確定] 儲存變更。  
  
     如果您使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範本資料庫和範本報表嘗試執行上述步驟，請注意只有 Company Sales 報表能夠直接使用 .odc 檔案。 其他範例報表包含無法處理 OLE DB 提供者的查詢參數和功能。 不過，您可以先在「報表設計師」中進行修改，使報表能夠使用 OLE DB 提供者。  
  
## <a name="see-also"></a>請參閱＜  
 [建立、修改和刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
