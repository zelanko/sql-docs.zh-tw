---
title: 將 DB2 資料移轉至 SQL Server (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f0ca7415952a9af6d3de84e66a41403070122888
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756186"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>將 DB2 資料移轉到 SQL Server (DB2ToSQL)
您已成功同步處理與已轉換的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以將資料從 DB2，以便移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 如果伺服器端資料移轉引擎所使用的引擎，然後，您可以將移轉資料之前您必須安裝 SSMA DB2 延伸模組組件和執行 SSMA 的電腦上的 DB2 提供者。 也必須執行的 SQL Server Agent 服務。 如需如何安裝此延伸模組組件的詳細資訊，請參閱[SQL Server 上安裝 SSMA 元件](http://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>移轉選項的設定  
然後再移轉資料到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，檢閱中的專案移轉選項**專案設定** 對話方塊。  
  
-   使用此對話方塊中，您可以設定選項，例如移轉批次大小、 資料表鎖定、 條件約束檢查，null 值的處理和身分識別值的處理。 如需將專案移轉設定的詳細資訊，請參閱[專案設定 （移轉）](http://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae)。  
  
-   **移轉引擎**中**專案設定**對話方塊，可讓使用者能夠執行使用的資料移轉引擎的兩種類型的移轉程序：  
  
    1.  用戶端端資料移轉引擎  
  
    2.  伺服器端資料移轉引擎  
  
**用戶端端資料移轉：**  
  
-   若要起始用戶端上的資料移轉，請選取**用戶端端資料移轉引擎**選項**專案設定** 對話方塊。  
  
-   在 **專案設定**，則**用戶端端資料移轉引擎**選項設定。  
  
    > [!NOTE]  
    > **用戶端資料移轉引擎**位於 SSMA 應用程式內，因此，就不相依於延伸模組套件的可用性。  
  
**伺服器端資料移轉：**  
  
-   在伺服器端資料移轉期間，引擎會位於目標資料庫。 它可透過延伸模組套件進行安裝。 如需有關如何安裝此延伸模組組件的詳細資訊，請參閱[SQL Server 上安裝 SSMA 元件](http://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   若要起始移轉的伺服器端上，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
## <a name="migrating-data-to-sql-server"></a>將資料移轉至 SQL Server  
移轉的資料會移至 DB2 資料表中的資料列的資料大量載入作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在交易中的資料表。 載入資料列數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]每一筆交易中已將專案設定中。  
  
若要檢視移轉訊息，請確定 [輸出] 窗格為可見。 否則，從**檢視**功能表上，選取**輸出**。  
  
**若要將資料移轉**  
  
1.  驗證下列項目：  
  
    -   執行 SSMA 的電腦上安裝的 DB2 提供者。  
  
    -   您已同步處理已轉換的物件與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
2.  在 DB2 中繼資料總管 中，選取包含您想要移轉之資料的物件：  
  
    -   若要將所有結構描述的資料移轉，選取核取方塊旁**結構描述**。  
  
    -   若要將資料移轉，或省略個別資料表，第一次展開結構描述中，依序展開**資料表**，然後選取或清除資料表旁邊的核取方塊。  
  
3.  若要將資料移轉，兩種情況下發生：  
  
    **用戶端端資料移轉：**  
  
    -   執行**用戶端端資料移轉**，選取**用戶端端資料移轉引擎**選項**專案設定** 對話方塊。  
  
    **伺服器端資料移轉：**  
  
    -   之前在伺服器端執行資料移轉，請確定：  
  
        1.  執行個體上安裝 SSMA for DB2 的延伸模組套件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
        2.  SQL Server 執行個體上執行的 SQL Server Agent 服務。  
  
    -   執行**伺服器端資料移轉**，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
4.  以滑鼠右鍵按一下**結構描述**在 DB2 中繼資料總管，然後按一下**移轉資料**。 您也可以移轉為個別物件或類別目錄的物件的資料： 以滑鼠右鍵按一下物件或其父資料夾;選取 **移轉資料**選項。  
  
    > [!NOTE]  
    > 如果執行個體上未安裝 SSMA for DB2 的延伸模組套件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且如果**伺服器端資料移轉引擎**已選取，然後同時將資料移轉到目標資料庫，發生下列錯誤: 'SQL Server 上找不到 SSMA 資料移轉的元件，無法進行伺服器端資料移轉。 請檢查是否已正確安裝延伸模組組件 '。 按一下 **取消**終止資料移轉。  
  
5.  在 [**連接到 DB2** ] 對話方塊中，輸入連線認證，然後再按一下**Connect**。 如需有關如何連接到 DB2 的詳細資訊，請參閱[連接至 DB2 資料庫&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    連接到目標資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，輸入中的連接認證**連接到 SQL Server**  對話方塊中，然後按一下**Connect**。 如需有關連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[連接到 SQL Server](http://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    訊息會出現在**輸出**窗格。 移轉完成時，**資料移轉報告**隨即出現。 如果未移轉任何資料，按一下包含錯誤，資料列，然後按一下**詳細資料**。 當您完成報表時，請按一下**關閉**。 如需有關資料移轉報告的詳細資訊，請參閱[（SSMA 常見） 的資料移轉報告](http://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 做為目標資料庫使用 SQL Express 版本時，允許只能用戶端端資料移轉，並不支援伺服器端資料移轉。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
