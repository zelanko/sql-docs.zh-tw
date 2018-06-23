---
title: Verify a PowerPivot for SharePoint 安裝 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
caps.latest.revision: 10
author: HeidiSteen
ms.author: heidist
manager: jhubbard
ms.openlocfilehash: 84457199c37eea8445911e25706928305db0d380
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023023"
---
# <a name="verify-a-powerpivot-for-sharepoint-installation"></a>確認 PowerPivot for SharePoint 安裝
  您在 SharePoint 伺服器陣列中安裝的 PowerPivot for SharePoint 執行個體是透過 SharePoint 管理中心來進行管理。 您至少可以檢查管理中心和 SharePoint 網站上的頁面，以確認 PowerPivot 伺服器元件和功能是可用的。 但是，為了完整確認安裝作業，您必須擁有可以發行到 SharePoint 並從文件庫存取的 PowerPivot 活頁簿。 為了測試用途，您可以發行已經包含 PowerPivot 資料的範例活頁簿，並用它來確認 SharePoint 整合已正確設定。  
  
##  <a name="verifyinstall"></a> 確認管理中心整合  
 若要確認 PowerPivot 可與管理中心整合，請執行下列動作：  
  
1.  在 開始 功能表上按一下**所有程式**，開啟 Microsoft SharePoint 2010 產品，然後按一下**SharePoint 2010 管理中心**。  
  
2.  輸入您的使用者名稱和密碼，然後按一下 [確定]。  
  
     您可以選擇修改瀏覽器設定，這樣一來，當您每次開啟管理中心時，就不必輸入使用者名稱和密碼。 若要將管理中心當做信任的網站加入，請執行下列動作。  
  
    1.  在 Internet Explorer 的 [工具] 功能表中，按一下 [網際網路選項]。  
  
    2.  在 [安全性] 索引標籤的 [選取要檢視或變更安全性設定的區域] 區段中，按一下 [信任的網站]，然後按一下 [網站]。  
  
    3.  清除 [此區域內的所有網站需要伺服器驗證 (https:)] 核取方塊。  
  
    4.  在 [將這個網站新增到區域] 中，輸入網站的 URL，然後按一下 [新增]。  
  
    5.  按一下 [關閉]，然後按一下 [確定]。  
  
        > [!NOTE]  
        >  SharePoint 安裝文件集包括用來解決 Proxy 伺服器錯誤以及停用 Internet Explorer 中 [增強式安全性設定] 的其他指示，好讓您可以下載及安裝更新。 如需詳細資訊，請參閱 Microsoft 網站上 **以 SQL Server 部署單一伺服器** 中的 " [Perform additional tasks](http://go.microsoft.com/fwlink/?LinkId=177754) " 一節。  
  
3.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列功能]**。  
  
4.  確認 **[PowerPivot 整合功能]** 為 **[使用中]**。  
  
5.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器上的服務]**。  
  
6.  確認 **SQL Server Analysis Services** 和 **SQL Server PowerPivot 系統服務** 都已啟動。  
  
7.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
8.  按一下**預設 PowerPivot 服務應用程式**此應用程式開啟 PowerPivot 管理儀表板。 在第一次使用時，需要數分鐘才能載入儀表板。  
  
     或者，按一下旁邊的空白空間**預設 PowerPivot 服務應用程式**選取資料列，然後按一下 **屬性**若要檢視此服務應用程式的組態設定。 您可以修改組態設定與應用程式屬性來變更您的伺服器組態。 如需有關這些設定的詳細資訊，請參閱[建立及設定 PowerPivot 服務應用程式，在 [管理中心]](../../power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)。  
  
## <a name="verify-integration-at-the-site-level"></a>確認網站層級的整合  
 若要確認 PowerPivot 可與 SharePoint 網站整合，請執行下列動作：  
  
1.  在瀏覽器中，開啟您建立的 Web 應用程式。 如果您使用預設值，您可以指定 http://\<您的電腦名稱 > 中的 URL 位址。  
  
2.  確認應用程式中可以使用 PowerPivot 資料存取和處理功能。 若要這樣做，您可以確認 PowerPivot 提供的文件庫範本是否存在：  
  
    1.  在 網站動作上按一下**更多選項...**.  
  
    2.  在程式庫，您應該會看到**資料摘要庫**和**PowerPivot 圖庫**。 這些文件庫範本是由 PowerPivot 功能所提供，如果此功能已正確整合，就可以在文件庫清單中看到這些範本。  
  
## <a name="verify-data-access-on-the-server"></a>確認伺服器上的資料存取。  
 若要在伺服器上確認 PowerPivot 資料存取，請執行以下作業：  
  
1.  [下載](http://go.microsoft.com/fwlink/?LinkID=219108) Reporting Services 教學課程隨附的野餐資料範例。 您將使用此下載中的範例活頁簿確認 PowerPivot 資料存取。 解壓縮檔案。  
  
2.  將 Excel 活頁簿 (.xlsx) 上傳至 Shared Documents。 此活頁簿包含內嵌的 PowerPivot 資料。  
  
3.  按一下文件，從文件庫中加以開啟。  
  
4.  按一下活頁簿頂端的交叉分析篩選器或篩選。 月份、色彩和類型是此活頁簿中的交叉分析篩選器。 按一下交叉分析篩選器會啟動 PowerPivot 查詢並證明您的伺服器可以運作。 伺服器將會在背景載入 PowerPivot 資料，然後傳回結果。  
  
5.  回到文件庫。 選取活頁簿右邊的向下箭號，然後按一下 [啟動 Power View]。 此步驟會確認 Reporting Services 中的 [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] 功能可以運作。 如果您未安裝 Reporting Services，請略過此步驟。  
  
     在下一個步驟中，您將會連接到 Management Studio 中的伺服器，並確認已經載入及快取資料。  
  
6.  在 [開始] 功能表中，從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 程式群組啟動 SQL Server Management Studio。 如果伺服器上未安裝此工具，您可以向前跳到最後一個步驟，確認快取檔案存在。  
  
7.  在 [伺服器類型] 中，選取 [Analysis Services]。  
  
8.  在 伺服器名稱輸入**\<伺服器名稱 > \powerpivot**，其中**\<伺服器名稱 >** 是具有 PowerPivot for SharePoint 安裝的電腦名稱。  
  
9. 按一下 **[連接]**。 這樣會確認可以使用 Analysis Services 伺服器。  
  
10. 在 [物件總管] 中，您可以按一下**資料庫**，檢視載入的 PowerPivot 資料檔案的清單。  
  
11. 在電腦檔案系統上，檢查下列資料夾來決定檔案是否要快取到磁碟。 快取檔案的存在會進一步驗證您的部署是否可以運作。 若要檢視檔案快取，請移至\<磁碟機 >: \Program Files\Microsoft SQL Server\MSAS11。POWERPIVOT\OLAP\Backup\Sandboxes\Default PowerPivot 服務應用程式資料夾。 每個快取的資料庫都會使用以 GUID 為基礎的命名慣例，儲存在自己的資料夾中，以確保名稱是唯一的。  
  
  