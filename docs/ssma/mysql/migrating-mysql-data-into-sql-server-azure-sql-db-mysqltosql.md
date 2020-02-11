---
title: 將 MySQL 資料移轉至 SQL Server-Azure SQL DB （MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 83a4a2d1bea5074cc268590d4074bde631f28694
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67908829"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>將 MySQL 資料移轉至 SQL Server-Azure SQL DB （MySQLToSQL）
當您成功地同步處理已轉換的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件與或 sql azure 之後，您可以將資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從 MYSQL 遷移到或 sql azure。  
  
> [!IMPORTANT]  
> 如果所使用的引擎是伺服器端資料移轉引擎，則在遷移資料之前，您必須在執行 SSMA 的電腦上安裝 SSMA for MySQL 延伸模組套件和 MySQL 提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務也必須正在執行。 如需有關如何安裝延伸模組套件的詳細資訊，請參閱[在 SQL Server 上安裝 SSMA 元件（MySQL 到 SQL）](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>設定遷移選項  
將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 之前，請在 [**專案設定**] 對話方塊中，檢查項目遷移選項。  
  
-   藉由使用此對話方塊，您可以設定選項，例如遷移批次大小、資料表鎖定、條件約束檢查、null 值處理和識別值處理。 如需專案遷移設定的詳細資訊，請參閱[專案設定（遷移）](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)。  
  
    如需有關**擴充資料移轉設定**的詳細資訊，請參閱[資料移轉設定](data-migration-settings-mysqltosql.md)  
  
-   [**專案設定**] 對話方塊中的 [**遷移引擎**] 可讓使用者使用兩種類型的資料移轉引擎來執行遷移程式：  
  
    1.  用戶端資料移轉引擎  
  
    2.  伺服器端資料移轉引擎  
  
**用戶端資料移轉：**  
  
-   若要在用戶端起始資料移轉，請在 [**專案設定**] 對話方塊中選取 [**用戶端資料移轉引擎**] 選項。  
  
-   在 [**專案設定**] 中，已設定 [**用戶端資料移轉引擎**] 選項。  
  
    > [!NOTE]  
    > **用戶端資料移轉引擎**位於 SSMA 應用程式內，因此不會相依于延伸模組套件的可用性。  
  
**伺服器端資料移轉：**  
  
-   在伺服器端資料移轉期間，引擎位於目標資料庫上。 它是透過延伸模組套件進行安裝。 如需有關如何安裝延伸模組套件的詳細資訊，請參閱[在 SQL Server 上安裝 SSMA 元件（MySQL 到 SQL）](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   若要在伺服器端起始遷移，請在 [**專案設定**] 對話方塊中選取 [**伺服器端資料移轉引擎**] 選項。  
  
> [!IMPORTANT]  
> **用戶端資料移轉**選項僅適用于 SQL Azure。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>將資料移轉至 SQL Server 或 SQL Azure  
遷移資料是大量載入作業，會將資料列從 MySQL 資料表移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或交易中的 SQL Azure 資料表。 在每個交易[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中載入的資料列數目，會在專案設定中設定。  
  
若要查看遷移訊息，請確定 [輸出] 窗格是可見的。 否則，請從 [ **View** ] 功能表選取 [**輸出**]。  
  
**遷移資料**  
  
1.  請確認下列事項：  
  
    -   MySQL 提供者會安裝在執行 SSMA 的電腦上。  
  
    -   您已將已轉換的物件與目標資料庫（SQL Server/SQL Azure）同步處理。  
  
2.  在 [MySQL 中繼資料瀏覽器] 中，選取包含您想要遷移之資料的物件：  
  
    -   若要遷移所有架構的資料，請選取 [**架構**] 旁的核取方塊。  
  
    -   若要遷移資料或省略個別的資料表，請先展開架構，展開 [**資料表**]，然後選取或清除資料表旁的核取方塊。  
  
3.  若要遷移資料，會發生兩種情況：  
  
    **用戶端資料移轉：**  
  
    -   若要執行**用戶端資料移轉**，請在 [**專案設定**] 對話方塊中選取 [**用戶端資料移轉引擎**] 選項。  
  
    **伺服器端資料移轉：**  
  
    -   在伺服器端執行資料移轉之前，請確定：  
  
        1.  SSMA for MySQL 延伸模組套件會安裝在 SQL Server 的實例上。  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務正在實例上執行 SQL Server  
  
    -   針對執行**伺服器端資料移轉**，請在 [**專案設定**] 對話方塊中選取 [**伺服器端資料移轉引擎**] 選項。  
  
4.  以滑鼠右鍵按一下 MySQL Metadata Explorer 中的 [**架構**]，然後按一下 [**遷移資料**]。 您也可以遷移個別物件或物件類別的資料：以滑鼠右鍵按一下物件或其父資料夾;選取 [**遷移資料**] 選項。  
  
    > [!NOTE]  
    > 如果 SQL Server 的實例上未安裝 SSMA for MySQL 延伸模組套件，而且已選取 [**伺服器端資料移轉引擎**]，則在將資料移轉至目標資料庫時，會發生下列錯誤：「在 SQL Server 上找不到 SSMA 資料移轉元件，將無法進行伺服器端資料移轉。 請檢查是否已正確安裝延伸模組套件」。 按一下 [**取消**] 以終止資料移轉。  
  
5.  在 [**連接到 MySQL** ] 對話方塊中，輸入連線認證，然後按一下 **[連接]**。 如需連線至 MySQL 的詳細資訊，請參閱連線[至 mysql &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    如果目標資料庫是 SQL Server，請在 [**連接到 SQL Server** ] 對話方塊中輸入連接認證，然後按一下 **[連接]**。 如需連接到 SQL Server 的詳細資訊，請參閱[連接到 SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    如果目標資料庫是 SQL Azure，請在 [**連接到 Sql azure** ] 對話方塊中輸入連接認證，然後按一下 **[連接]**。 如需有關連接到 SQL Azure 的詳細資訊，請參閱[連接到 AZURE SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    訊息將會出現在 [**輸出**] 窗格中。 當遷移完成時，就會顯示**資料移轉報表**。 如果有任何資料未遷移，請按一下包含錯誤的資料列，然後按一下 [**詳細**資料]。 當您完成報表時，請按一下 [**關閉**]。 如需資料移轉報告的詳細資訊，請參閱[資料移轉報告（SSMA 一般）](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 當 SQL Express edition 做為目標資料庫使用時，只允許用戶端資料移轉，而且不支援伺服器端資料移轉。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
