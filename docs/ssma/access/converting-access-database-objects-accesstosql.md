---
title: 轉換 Access 資料庫物件 (AccessToSQL) |Microsoft Docs
description: 瞭解如何在連接到 SQL Server/Azure SQL Database 之後選取存取資料庫物件，然後將架構轉換成 SQL Server/SQL Database 架構。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 04f6f0adb61a0bb7ccf33e3705a4a32b9ed9d69e
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988224"
---
# <a name="converting-access-database-objects-accesstosql"></a>轉換 Access 資料庫物件 (AccessToSQL) 
在您新增 Access 資料庫並連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 之後，SSMA 會顯示存取權和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 物件的中繼資料。 您現在可以選取 [存取資料庫物件]，然後將架構轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 架構。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從存取中繼資料取得物件定義、將它們轉換成相等 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的語法，然後將此資訊載入至專案。 然後，您可以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql Azure Metadata Explorer 來查看或 sql azure 物件及其屬性。  
  
> [!IMPORTANT]  
> 轉換物件不會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 中建立物件。 它只會轉換物件定義，並將資訊儲存在 SSMA 專案中。  
  
在轉換期間，SSMA 會將狀態列印到 [輸出] 窗格，並將 [錯誤]、[警告] 和 [資訊訊息] 列印到 [錯誤清單] 窗格。 使用此資訊來判斷您是否需要修改 Access 資料庫或轉換程式，以取得所需的轉換結果。 您也可以使用「 [準備 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md) 中的資料移轉」主題中的資訊，來判斷哪些內容將不會轉換。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
轉換物件之前，請在 [ **專案設定** ] 對話方塊中檢查項目轉換選項。 您可以使用此對話方塊來設定 SSMA 如何轉換索引備忘錄資料行、主鍵、外鍵條件約束、時間戳記和沒有索引的資料表。 如需詳細資訊，請參閱 [專案設定 (轉換) ](./project-settings-conversion-accesstosql.md)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示已轉換的存取物件，以及產生的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 物件：  
  
|存取物件|產生的 SQL Server 物件|  
|-----------------|-------------------------------|  
|資料表|資料表|  
|直條圖|直條圖|  
|索引|索引|  
|外部索引鍵 (foreign key)|外部索引鍵 (foreign key)|  
|查詢|檢視<br /><br />大部分的選取查詢都會轉換成 views。 其他查詢（例如 UPDATE 查詢）則不會遷移。<br /><br />使用參數的 SELECT 查詢不會轉換，也不會有交叉索引標籤的查詢。|  
|報表|未轉換|  
|表單|未轉換|  
|巨集|未轉換|  
|name|未轉換|  
|預設值|預設值|  
|允許長度為零的資料行屬性|check 條件約束|  
|資料行驗證規則|check 條件約束|  
|資料表驗證規則|check 條件約束|  
|主索引鍵 (primary key)|主索引鍵 (primary key)|  
  
## <a name="converting-access-objects"></a>轉換 Access 物件  
若要轉換 Access 資料庫物件，您必須先選取要轉換的物件，然後讓 SSMA 進行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [ **輸出**]。  
  
**選取和轉換 Access 資料庫物件至 SQL Server 或 SQL Azure 語法**  
  
1.  在 [Access Metadata Explorer] 中，展開 [ **存取-元**資料]，然後展開 [ **資料庫**]。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要轉換所有資料庫，請選取 [ **資料庫**] 旁的核取方塊。  
  
    -   若要轉換或省略個別資料庫，請選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或省略查詢，請展開資料庫，然後選取或清除 [ **查詢** ] 核取方塊。  
  
    -   若要轉換或省略個別資料表，請展開資料庫，展開 [ **資料表**]，然後選取或清除資料表旁的核取方塊。  
  
3.  執行下列其中一個動作：  
  
    -   若要轉換架構，請以滑鼠右鍵按一下 [ **資料庫** ]，然後選取 [ **轉換架構**]。  
  
        您也可以轉換個別的物件。 若要轉換物件，不論選取哪一個物件，以滑鼠右鍵按一下物件，然後選取 [ **轉換架構**]。  
  
        當物件已轉換時，在 Access Metadata Explorer 中會顯示為粗體。  
  
    -   若要在一個步驟中轉換、載入及遷移架構和資料，請以滑鼠右鍵按一下 [資料庫]，然後選取 [ **轉換]、[載入] 和 [遷移**]。  
  
4.  查看 [ **輸出** ] 窗格中的訊息，以及 [ **錯誤清單** ] 窗格中的任何錯誤和警告。  
  
## <a name="altering-tables-and-indexes"></a>改變數據表和索引  
將存取中繼資料轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 中繼資料，以及將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 之前，您可以改變 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 資料表和索引。  
  
**若要改變數據表或索引屬性**  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 中繼資料瀏覽器中，選取您要變更的資料表或索引。  
  
2.  在 [ **資料表** ] 索引標籤上，按一下您要變更的屬性，然後輸入或選取新的設定。 例如，您可以將 Nvarchar (15) 變更為 Nvarchar (20) ，或選取核取方塊讓資料表資料行變成可為 null。  
  
    將游標移出已變更的屬性儲存格。 若要這麼做，您可以按一下另一個資料列，或按下 Tab 鍵。  
  
3.  按一下 [套用]。  
  
您現在可以在 [ **SQL** ] 索引標籤上，查看程式碼中的變更。  
  
## <a name="next-steps"></a>後續步驟  
遷移程式的下一個步驟是將 [資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
