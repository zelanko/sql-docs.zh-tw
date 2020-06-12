---
title: 將 DB2 資料移轉至 SQL Server （DB2ToSQL） |Microsoft Docs
description: 瞭解如何在同步處理已轉換的物件之後，將資料從 DB2 資料庫移轉至 SQL Server 或 Azure SQL Database。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 408bf80b8c8a6f70488333f476422dedb9db1887
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293965"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>將 DB2 資料移轉至 SQL Server （DB2ToSQL）
當您成功地同步處理已轉換的物件之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以將資料從 DB2 遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
> [!IMPORTANT]  
> 如果所使用的引擎是伺服器端資料移轉引擎，則在您可以遷移資料之前，您必須在執行 SSMA 的電腦上安裝 SSMA for DB2 Extension Pack 和 DB2 提供者。 SQL Server Agent 服務也必須正在執行。 如需有關如何安裝延伸模組套件的詳細資訊，請參閱[在 SQL Server 上安裝 SSMA 元件](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>設定遷移選項  
將資料移轉至之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請在 [**專案設定**] 對話方塊中，檢查項目遷移選項。  
  
-   藉由使用此對話方塊，您可以設定選項，例如遷移批次大小、資料表鎖定、條件約束檢查、null 值處理和識別值處理。 如需專案遷移設定的詳細資訊，請參閱[專案設定（遷移）](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae)。  
  
-   [**專案設定**] 對話方塊中的 [**遷移引擎**] 可讓使用者使用兩種類型的資料移轉引擎來執行遷移程式：  
  
    1.  用戶端資料移轉引擎  
  
    2.  伺服器端資料移轉引擎  
  
**用戶端資料移轉：**  
  
-   若要在用戶端起始資料移轉，請在 [**專案設定**] 對話方塊中選取 [**用戶端資料移轉引擎**] 選項。  
  
-   在 [**專案設定**] 中，已設定 [**用戶端資料移轉引擎**] 選項。  
  
    > [!NOTE]  
    > **用戶端資料移轉引擎**位於 SSMA 應用程式內，因此不會相依于延伸模組套件的可用性。  
  
**伺服器端資料移轉：**  
  
-   在伺服器端資料移轉期間，引擎位於目標資料庫上。 它是透過延伸模組套件進行安裝。 如需有關如何安裝延伸模組套件的詳細資訊，請參閱[在 SQL Server 上安裝 SSMA 元件](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   若要在伺服器端起始遷移，請在 [**專案設定**] 對話方塊中選取 [**伺服器端資料移轉引擎**] 選項。  
  
## <a name="migrating-data-to-sql-server"></a>將資料移轉至 SQL Server  
遷移資料是大量載入作業，可將 DB2 資料表中的資料列移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易中的資料表。 在每個交易中載入的資料列數目 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，會在專案設定中設定。  
  
若要查看遷移訊息，請確定 [輸出] 窗格是可見的。 否則，請從 [ **View** ] 功能表選取 [**輸出**]。  
  
**遷移資料**  
  
1.  驗證下列項目：  
  
    -   DB2 提供者會安裝在執行 SSMA 的電腦上。  
  
    -   您已將已轉換的物件與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫同步處理。  
  
2.  在 [DB2 中繼資料瀏覽器] 中，選取包含您要遷移之資料的物件：  
  
    -   若要遷移所有架構的資料，請選取 [**架構**] 旁的核取方塊。  
  
    -   若要遷移資料或省略個別的資料表，請先展開架構，展開 [**資料表**]，然後選取或清除資料表旁的核取方塊。  
  
3.  若要遷移資料，會發生兩種情況：  
  
    **用戶端資料移轉：**  
  
    -   若要執行**用戶端資料移轉**，請在 [**專案設定**] 對話方塊中選取 [**用戶端資料移轉引擎**] 選項。  
  
    **伺服器端資料移轉：**  
  
    -   在伺服器端執行資料移轉之前，請確定：  
  
        1.  SSMA for DB2 延伸模組套件會安裝在實例上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
        2.  SQL Server Agent 服務正在 SQL Server 的實例上執行。  
  
    -   針對執行**伺服器端資料移轉**，請在 [**專案設定**] 對話方塊中選取 [**伺服器端資料移轉引擎**] 選項。  
  
4.  以滑鼠右鍵按一下 DB2 Metadata Explorer 中的 [**架構**]，然後按一下 [**遷移資料**]。 您也可以遷移個別物件或物件類別的資料：以滑鼠右鍵按一下物件或其父資料夾;選取 [**遷移資料**] 選項。  
  
    > [!NOTE]  
    > 如果的實例上未安裝 SSMA for DB2 延伸模組套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且已選取 [**伺服器端資料移轉引擎**]，則在將資料移轉至目標資料庫時，會發生下列錯誤：「在 SQL Server 上找不到 SSMA 資料移轉元件，將無法進行伺服器端資料移轉。 請檢查是否已正確安裝延伸模組套件」。 按一下 [**取消**] 以終止資料移轉。  
  
5.  在 [**連接到 DB2** ] 對話方塊中，輸入連接認證，然後按一下 **[連接]**。 如需連接到 DB2 的詳細資訊，請參閱[連接到 Db2 資料庫 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    若要連接到目標資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請在 [**連接到 SQL Server** ] 對話方塊中輸入連接認證，然後按一下 [**連接]**。 如需有關連接到的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[連接到 SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    訊息將會出現在 [**輸出**] 窗格中。 當遷移完成時，就會顯示**資料移轉報表**。 如果有任何資料未遷移，請按一下包含錯誤的資料列，然後按一下 [**詳細**資料]。 當您完成報表時，請按一下 [**關閉**]。 如需資料移轉報告的詳細資訊，請參閱[資料移轉報告（SSMA 一般）](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 當 SQL Express edition 做為目標資料庫使用時，只允許用戶端資料移轉，而且不支援伺服器端資料移轉。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
