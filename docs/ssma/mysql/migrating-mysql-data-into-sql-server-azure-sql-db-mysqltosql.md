---
title: 將 MySQL 資料移轉到 SQL Server-Azure SQL DB (MySQLToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bef9d72e855f70d520323950b789c1c330bcde4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>將 MySQL 資料移轉到 SQL Server-Azure SQL DB (MySQLToSQL)
已成功同步處理與已轉換的物件之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您可以移轉的資料從 MySQL 至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
> [!IMPORTANT]  
> 如果引擎正在使用伺服器端資料移轉引擎，然後，然後再移轉資料，您必須安裝的 SSMA for MySQL 擴充功能組件並執行 SSMA 的電腦上的 MySQL 提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]也必須執行代理程式服務。 如需如何安裝延伸模組組件的詳細資訊，請參閱[SSMA 元件安裝 SQL Server (MySQL to SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>移轉選項的設定  
然後再移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中，檢閱中的專案移轉選項**專案設定** 對話方塊。  
  
-   使用此對話方塊中，您可以設定選項，例如移轉批次大小、 鎖定資料表、 條件約束檢查，null 值的處理和識別值處理。 如需專案移轉設定的詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)。  
  
    如需有關**擴充資料移轉設定**，請參閱[資料移轉設定](http://msdn.microsoft.com/en-us/9c396df4-5676-4f32-9c57-70d4f15f9b7a)  
  
-   **移轉引擎**中**專案設定**對話方塊，可讓使用者執行移轉程序，使用兩種類型的資料移轉引擎：  
  
    1.  用戶端資料移轉引擎  
  
    2.  伺服器端資料移轉引擎  
  
**用戶端端資料移轉：**  
  
-   若要起始用戶端上的資料移轉，選取**用戶端資料移轉引擎**選項**專案設定** 對話方塊。  
  
-   在**專案設定**、**用戶端資料移轉引擎**選項設定。  
  
    > [!NOTE]  
    > **用戶端資料移轉引擎**位於 SSMA 應用程式內，而且是的因此，不依存於此延伸模組組件的可用性。  
  
**伺服器端資料移轉：**  
  
-   在伺服器端資料移轉期間，引擎會位於目標資料庫。 它是透過擴充功能套件安裝。 如需有關如何安裝延伸模組組件的詳細資訊，請參閱[SSMA 元件安裝 SQL Server (MySQL to SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   若要起始移轉的伺服器端上，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
> [!IMPORTANT]  
> **用戶端端資料移轉**選項僅適用於 SQL Azure。  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>將資料移轉至 SQL Server 或 SQL Azure  
移轉資料是從 MySQL 資料表到移動的資料列大量載入作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表在交易中的。 載入資料列數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]每一筆交易中設定專案設定中。  
  
若要檢視移轉訊息，請確定輸出窗格已顯示。 否則，從**檢視**功能表上，選取**輸出**。  
  
**若要將資料移轉**  
  
1.  驗證下列項目：  
  
    -   MySQL 提供者會執行 SSMA 的電腦上安裝。  
  
    -   您有與目標資料庫同步處理已轉換的物件 (SQL Server / SQL Azure)。  
  
2.  在 MySQL 中繼資料總管，選取包含您想要移轉之資料的物件：  
  
    -   若要將所有結構描述的資料移轉，選取核取方塊旁的 **結構描述**。  
  
    -   若要將資料移轉，或省略個別資料表，第一次展開結構描述中，展開**資料表**，然後選取或清除資料表旁的核取方塊。  
  
3.  若要將資料移轉，兩種情況下發生：  
  
    **用戶端端資料移轉：**  
  
    -   執行**用戶端端資料移轉**，選取**用戶端資料移轉引擎**選項**專案設定** 對話方塊。  
  
    **伺服器端資料移轉：**  
  
    -   在伺服器端執行資料移轉之前, 請確定：  
  
        1.  SSMA for MySQL 擴充功能組件被安裝在 SQL Server 執行個體上。  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式服務正在 SQL Server 執行個體上執行  
  
    -   執行**伺服器端資料移轉**，選取**伺服器端資料移轉引擎**選項**專案設定** 對話方塊。  
  
4.  以滑鼠右鍵按一下**結構描述**中 MySQL 中繼資料總管，然後按一下**移轉資料**。 您也可以移轉資料的個別物件或類別目錄的物件： 以滑鼠右鍵按一下物件或其父資料夾。選取**移轉資料**選項。  
  
    > [!NOTE]  
    > 如果 SQL Server 執行個體上未安裝的 SSMA for MySQL 擴充功能組件，而且**伺服器端資料移轉引擎**已選取，然後同時將資料移轉到目標資料庫，發生下列錯誤: ' SSMA 資料移轉元件找不到 SQL Server 上無法進行伺服器端資料移轉。 請檢查是否已正確安裝延伸模組組件 '。 按一下**取消**終止資料移轉。  
  
5.  在**連接到 MySQL**對話方塊中，輸入連接的認證，然後按一下**連接**。 如需有關如何連接至 MySQL 的詳細資訊，請參閱[連接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    如果目標資料庫是 SQL Server，然後輸入中的連接認證**連接到 SQL Server**對話方塊中，然後按一下**連接**。 如需有關如何連接到 SQL Server 的詳細資訊，請參閱[連接到 SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    如果目標資料庫是 SQL Azure，然後輸入中的連接認證**連接到 SQL Azure**對話方塊中，然後按一下**連接**。 如需有關如何連接到 SQL Azure 的詳細資訊，請參閱[連接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    訊息會出現在**輸出**窗格。 移轉完成時，**資料移轉報告**隨即出現。 如果沒有不會移轉任何資料，按一下包含錯誤的資料列，然後按一下**詳細資料**。 當您不再使用的報表時，請按一下 **關閉**。 如需有關資料移轉報告的詳細資訊，請參閱[（SSMA 通用） 的資料移轉報告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express edition 做為目標資料庫使用時，允許只有用戶端端資料移轉，且不支援伺服器端資料移轉。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
