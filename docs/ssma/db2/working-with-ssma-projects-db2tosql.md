---
title: 使用 SSMA 專案 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d3ccc9fe24d770fa64b2bef86feabab0dd2e7fba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63244660"
---
# <a name="working-with-ssma-projects-db2tosql"></a>使用 SSMA 專案 (DB2ToSQL)
若要將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您首先建立 SSMA 專案。 專案是檔案，其中包含下列資訊：  
  
-   您想要移轉至 DB2 資料庫的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   目標執行個體的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，將會收到已移轉的物件和資料。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊。  
  
-   專案設定。  
  
當您開啟專案時，它已中斷連線從 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可讓您離線工作。 如需有關重新連線到資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 連接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)。</c2>  
  
## <a name="reviewing-default-project-settings"></a>檢閱預設的專案設定  
SSMA 會包含數個設定的轉換和載入資料庫物件、 移轉資料，以及與 DB2 同步處理 SSMA 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 預設設定是適用於許多使用者。 不過，您建立新的 SSMA 專案之前，您應該檢閱設定。 如果您想要您可以變更將會用於所有新專案的預設設定。  
  
**若要檢視預設的專案設定**  
  
1.  在 **工具**功能表上，按一下**預設專案設定**。  
  
2.  選取專案類型，在**遷移目標版本**可才能檢視或變更哪些設定，然後按一下向下的距離**一般** 索引標籤。  
  
3.  在左窗格中，按一下 **轉換**。  
  
4.  在右窗格中，請檢閱並視需要變更設定。 如需有關這些設定的詳細資訊，請參閱 <<c0> [ 專案設定&#40;轉換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)。</c0>  
  
5.  重複步驟 1-3 的移轉、 同步處理，正在載入系統物件、 GUI 和類型對應的頁面。  
  
    -   移轉設定的相關資訊，請參閱[專案設定&#40;移轉&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)。  
  
    -   系統物件設定的相關資訊，請參閱[專案設定&#40;載入系統物件&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)。  
  
    -   如需設定進行同步處理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 專案設定&#40;同步處理&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。</c2>  
  
    -   GUI 設定的相關資訊，請參閱[專案設定&#40;GUI&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)。  
  
    -   如需資料類型對應設定的資訊，請參閱[專案設定&#40;類型對應&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)。  
  
## <a name="creating-new-projects"></a>建立新專案  
若要將資料從 DB2 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須先建立專案。  
  
**若要建立專案**  
  
1.  在 **檔案**功能表上，按一下**新的專案**。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 **名稱**方塊中，輸入您專案的名稱。  
  
3.  在 **位置**方塊中，輸入或選取專案的資料夾，然後按一下**確定**。  
  
4.  在**遷移至**下拉式清單，請選取目標版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移所使用的。 可用的選項如下：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL DB  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義套用到所有新的 SSMA 專案的預設專案設定，您可以自訂每個專案的設定。 如需詳細資訊，請參閱 <<c0> [ 設定專案選項&#40;OracleToSQL&#41; ](../../ssma/oracle/setting-project-options-oracletosql.md)和相關的區段。</c0>  
  
當您自訂來源和目標資料庫之間的資料型別對應時，您可以定義在專案、 資料庫或物件層級的對應。 如需詳細資訊，請參閱 <<c0> [ 對應 DB2 和 SQL Server 資料類型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。</c0>  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，專案設定，並選擇性地資料庫中繼資料中的，專案檔，也將會保留 SSMA。  
  
**若要儲存專案**  
  
-   在 **檔案**功能表上，按一下**儲存專案**。  
  
    如果專案中的結構描述已變更，或尚未轉換，SSMA 會提示您載入和儲存中繼資料。 載入和儲存中繼資料可讓您離線工作。 它也可讓您將完成的專案檔傳送給其他人，例如技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  顯示狀態為每個結構描述**中繼資料遺漏**，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料，可能需要幾分鐘的時間。 如果您不想儲存中繼資料，但不選取任何核取方塊。  
  
    2.  按一下 [儲存]  按鈕。  
  
        SSMA 會剖析 DB2 結構描述，並將中繼資料儲存到專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它已中斷連線從 DB2 及[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 可讓您離線工作。 若要更新的中繼資料，資料庫物件載入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要將資料移轉，您必須重新連線至 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在上**檔案**功能表上，指向**最近使用的專案**，然後按一下您想要開啟的專案。  
  
    -   在 **檔案**功能表上，選取**開啟專案**，找出.o2ssproj 專案檔中，選取檔案，，然後按一下**開啟**。  
  
2.  在重新連線到 DB2**檔案**功能表上，按一下**重新連接至 DB2**。  
  
3.  若要重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上**檔案**功能表上，按一下**重新連接到 SQL Server**。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接至 DB2 資料庫](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 DB2 資料庫到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[連接至 DB2 資料庫&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[連接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
