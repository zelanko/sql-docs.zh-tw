---
title: "建立及管理專案 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f26e8ea69db09f6eedd1af6682fbc5cbca558bab
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="creating-and-managing-projects-accesstosql"></a>建立及管理專案 (AccessToSQL)
若要將 Access 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您必須先建立的 SSMA 專案。 專案是包含您想要移轉至 Access 資料庫的相關中繼資料的檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，目標執行個體的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 移轉的物件和資料，將會接收[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]連接資訊和專案設定。  
  
## <a name="reviewing-default-project-settings"></a>檢閱預設的專案設定  
SSMA 會包含轉換和同步處理資料庫物件以及將資料轉換的數個選項。 這些選項的預設值是適用於許多使用者。 不過，在建立新的 SSMA 專案之前，您應該檢閱的選項，如果您想要的變更將用於所有新專案的預設設定。  
  
**若要檢閱預設的專案設定**  
  
1.  在**工具**功能表上，選取**預設專案設定**。  
  
2.  選取 [專案類型中的**移轉的目標版本**下拉式清單可檢視 / 變更哪些設定，然後按一下**一般**] 索引標籤。  
  
3.  在左窗格中，按一下 **轉換**。  
  
4.  在右窗格中，檢閱選項。 如需有關這些選項的詳細資訊，請參閱[（轉換） 的專案設定](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)。  
  
5.  視需要變更選項。  
  
6.  重複上述步驟的**移轉**， **GUI**，和**類型對應**頁面。  
  
    -   移轉選項的相關資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。  
  
    -   如需使用者介面選項的資訊，請參閱[專案設定 (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
    -   如需資料類型對應設定的詳細資訊，請參閱[（型別對應） 的專案設定](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)。  
  
    -   設定 SQL Azure 的相關資訊，請參閱[專案設定 (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e)。  
  
**請注意**只有當您選取移轉至 SQL Azure 建立的專案時，SQL Azure 設定將會使用。  
  
## <a name="creating-new-projects"></a>建立新的專案  
SSMA 會啟動但不載入預設專案。 若要將資料從 Access 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您必須建立專案。  
  
**若要建立新的專案**  
  
1.  在 [檔案] 功能表上，選取 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在**名稱**方塊中，輸入您的專案名稱。  
  
3.  在**位置**方塊中，輸入或選取專案的資料夾  
  
4.  移轉到下拉式清單中向下，選取其中一個 SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL 資料庫，然後按一下 **確定**。  
  
SSMA 會建立專案檔。 您現在可以執行的下一個步驟[新增一或多個 Access 資料庫](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義預設專案設定將套用到所有新的 SSMA 專案，您也可以自訂每個專案的設定。 如需詳細資訊，請參閱[設定轉換和移轉選項](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167)。  
  
當您自訂來源和目標資料庫之間的資料類型對應時，您可以定義在專案、 資料庫或物件層級的對應。 如需型別對應的詳細資訊，請參閱[對應來源和目標資料型別](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，SSMA 保存專案設定，並選擇性地資料庫中繼資料，加入專案檔。  
  
**若要儲存專案**  
  
-   在**檔案**功能表上，選取**儲存專案**。  
  
    如果在專案中的資料庫已變更或尚未轉換，SSMA 會提示您，將中繼資料儲存至專案。 儲存中繼資料，可讓您離線工作。 它也可讓您將完成的專案檔案傳送給其他人，包括技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  每個資料庫的狀態是 **中繼資料遺漏**，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料，可能需要幾分鐘的時間。 如果不想此時儲存中繼資料，請勿選取任何核取方塊。  
  
    2.  按一下 **[儲存]**。  
  
        SSMA 會剖析存取結構描述，並將中繼資料儲存到專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它已中斷連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 這可讓您離線工作。 若要更新中繼資料載入資料庫物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 若要將資料移轉，您必須重新連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
**若要開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在**檔案**功能表上，指向**最近使用的專案**，然後選取您想要開啟專案。  
  
    -   在**檔案**功能表上，選取**開啟專案**、 尋找.a2ssproj 專案檔中，選取檔案，並按一下**開啟**。  
  
2.  若要重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]上**檔案**功能表上，選取**重新連接到 SQL Server**。  
  
3.  若要重新連線到 SQL Azure 上**檔案**功能表上，選取**重新連線到 SQL Azure。**  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[新增一或多個 Access 資料庫](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)。  
  
## <a name="see-also"></a>請參閱＜  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[加入和移除 Access 資料庫檔案](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
