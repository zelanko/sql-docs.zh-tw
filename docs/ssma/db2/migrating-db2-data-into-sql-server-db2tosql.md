---
title: "將 DB2 資料移轉至 SQL Server (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 392deeac6aeb1791322723367def8f2e3e6464e8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>將 DB2 資料移轉至 SQL Server (DB2ToSQL)
已成功同步處理與已轉換的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可以將資料移轉至 DB2 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 如果伺服器端資料移轉引擎所使用的引擎，然後，您可以移轉的資料，您必須先安裝 SSMA DB2 延伸模組組件和執行 SSMA 的電腦上的 DB2 提供者。 也必須執行 SQL Server Agent 服務。 如需如何安裝延伸模組組件的詳細資訊，請參閱[安裝 SQL Server 上的 SSMA 元件](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>移轉選項的設定  
然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，檢閱中的專案移轉選項**專案設定** 對話方塊。  
  
-   使用此對話方塊中，您可以設定選項，例如移轉批次大小、 資料表鎖定、 條件約束檢查，null 值的處理，以及識別值處理。 如需專案移轉設定的詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae)。  
  
-   **移轉引擎**中**專案設定**對話方塊，可讓使用者執行移轉程序，使用兩種類型的資料移轉引擎：  
  
    1.  用戶端資料移轉引擎  
  
    2.  伺服器端資料移轉引擎  
  
**用戶端端資料移轉：**  
  
-   若要起始用戶端上的資料移轉，選取**用戶端資料移轉引擎**選項**專案設定** 對話方塊。  
  
-   在**專案設定**、**用戶端資料移轉引擎**選項設定。  
  
    > [!NOTE]  
    > **用戶端資料移轉引擎**位於 SSMA 應用程式內，而且是的因此，不依存於此延伸模組組件的可用性。  
  
**伺服器端資料移轉：**  
  
-   在伺服器端資料移轉期間，引擎會位於目標資料庫。 它是透過擴充功能套件安裝。 如需有關如何安裝延伸模組組件的詳細資訊，請參閱[安裝 SQL Server 上的 SSMA 元件](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   若要起始移轉的伺服器端上，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
## <a name="migrating-data-to-sql-server"></a>將資料移轉至 SQL Server  
移轉資料是將資料列移到 DB2 資料表中大量載入作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在交易中的資料表。 載入資料列數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]每一筆交易中設定專案設定中。  
  
若要檢視移轉訊息，請確定輸出窗格已顯示。 否則，從**檢視**功能表上，選取**輸出**。  
  
**若要將資料移轉**  
  
1.  驗證下列項目：  
  
    -   SSMA 執行電腦上安裝的 DB2 提供者。  
  
    -   您已同步處理已轉換的物件與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
2.  在 DB2 中繼資料總管，選取包含您想要移轉之資料的物件：  
  
    -   若要將所有結構描述的資料移轉，選取核取方塊旁的 **結構描述**。  
  
    -   若要將資料移轉，或省略個別資料表，第一次展開結構描述中，展開**資料表**，然後選取或清除資料表旁的核取方塊。  
  
3.  若要將資料移轉，兩種情況下發生：  
  
    **用戶端端資料移轉：**  
  
    -   執行**用戶端端資料移轉**，選取**用戶端資料移轉引擎**選項**專案設定** 對話方塊。  
  
    **伺服器端資料移轉：**  
  
    -   在伺服器端執行資料移轉之前, 請確定：  
  
        1.  SSMA for DB2 延伸模組組件已安裝的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
        2.  SQL Server Agent 服務正在執行的 SQL Server 執行個體上。  
  
    -   執行**伺服器端資料移轉**，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
4.  以滑鼠右鍵按一下**結構描述**在 DB2 中繼資料總管，然後按一下**移轉資料**。 您也可以移轉資料的個別物件或類別目錄的物件： 以滑鼠右鍵按一下物件或其父資料夾。選取**移轉資料**選項。  
  
    > [!NOTE]  
    > 如果執行個體上未安裝 DB2 延伸模組組件的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，如果**伺服器端資料移轉引擎**已選取，然後同時將資料移轉到目標資料庫，發生下列錯誤: ' SSMA 資料移轉元件找不到 SQL Server 上無法進行伺服器端資料移轉。 請檢查是否已正確安裝延伸模組組件 '。 按一下**取消**終止資料移轉。  
  
5.  在**連接到 DB2**對話方塊中，輸入連接的認證，然後按一下**連接**。 如需有關如何連接到 DB2 的詳細資訊，請參閱[連接到 DB2 資料庫 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    連接到目標資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，輸入中的連接認證**連接到 SQL Server**對話方塊中，然後按一下**連接**。 如需有關連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱[連接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    訊息會出現在**輸出**窗格。 移轉完成時，**資料移轉報告**隨即出現。 如果沒有不會移轉任何資料，按一下包含錯誤的資料列，然後按一下**詳細資料**。 當您不再使用的報表時，請按一下 **關閉**。 如需有關資料移轉報告的詳細資訊，請參閱[（SSMA 通用） 的資料移轉報告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express edition 做為目標資料庫使用時，允許只有用戶端端資料移轉，且不支援伺服器端資料移轉。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  

