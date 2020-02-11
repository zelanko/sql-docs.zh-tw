---
title: 轉換 Access 資料庫物件（AccessToSQL） |Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 56c55dbc5df61bfdb9013e505335af16fccbeecd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006626"
---
# <a name="converting-access-database-objects-accesstosql"></a>轉換 Access 資料庫物件（AccessToSQL）
在您加入 Access 資料庫並聯機到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 之後，SSMA 會顯示存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 資料庫物件的中繼資料。 您現在可以選取 [存取資料庫物件]，然後將架構轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成或 SQL Azure 架構。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從存取中繼資料取得物件定義，將它們轉換成[!INCLUDE[tsql](../../includes/tsql-md.md)]相等的語法，然後將這些資訊載入專案。 接著，您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Sql azure 中繼資料 Explorer，來查看或 sql azure 物件及其屬性。  
  
> [!IMPORTANT]  
> 轉換物件並不會在或 SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 中建立物件。 它只會轉換物件定義，並將資訊儲存在 SSMA 專案中。  
  
轉換期間，SSMA 會將狀態列印到 [輸出] 窗格，以及 [錯誤]、[警告] 和 [告知性訊息] 至 [錯誤清單] 窗格。 使用此資訊來判斷您是否需要修改 Access 資料庫或轉換程式，以取得所需的轉換結果。 您也可以使用[準備存取資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)主題中的資訊，以判斷將不會轉換哪些內容。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換物件之前，請先查看 [**專案設定**] 對話方塊中的 [專案轉換] 選項。 藉由使用此對話方塊，您可以設定 SSMA 如何轉換索引的備忘資料行、主鍵、外鍵條件約束、時間戳記和沒有索引的資料表。 如需詳細資訊，請參閱[專案設定（轉換）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示要轉換哪些存取物件，以及產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的或 SQL Azure 物件：  
  
|存取物件|產生 SQL Server 物件|  
|-----------------|-------------------------------|  
|資料表|資料表|  
|column|column|  
|索引|索引|  
|外部索引鍵 (foreign key)|外部索引鍵 (foreign key)|  
|查詢|檢視<br /><br />大部分的 SELECT 查詢都會轉換成 views。 其他查詢，例如更新查詢，則不會遷移。<br /><br />不會轉換接受參數的 SELECT 查詢，也不會交叉索引標籤的查詢。|  
|report|未轉換|  
|form|未轉換|  
|巨集|未轉換|  
|module|未轉換|  
|預設值|預設值|  
|允許長度為零的資料行屬性|檢查條件約束|  
|資料行驗證規則|檢查條件約束|  
|資料表驗證規則|檢查條件約束|  
|主索引鍵 (primary key)|主索引鍵 (primary key)|  
  
## <a name="converting-access-objects"></a>轉換存取物件  
若要轉換 Access 資料庫物件，您必須先選取要轉換的物件，然後讓 SSMA 執行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [**輸出**]。  
  
**選取並將 Access 資料庫物件轉換成 SQL Server 或 SQL Azure 語法**  
  
1.  在 [存取中繼資料瀏覽器] 中，展開 [**存取-資料庫**]，然後展開 [**資料庫**]。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要轉換所有資料庫，請選取 [**資料庫**] 旁的核取方塊。  
  
    -   若要轉換或省略個別資料庫，請選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或省略查詢，請展開資料庫，然後選取或清除 [**查詢**] 核取方塊。  
  
    -   若要轉換或省略個別資料表，請展開資料庫，展開 [**資料表**]，然後選取或清除資料表旁的核取方塊。  
  
3.  執行下列其中一個動作：  
  
    -   若要轉換架構，請以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**轉換架構**]。  
  
        您也可以轉換個別物件。 若要轉換物件，不論選取的物件為何，請以滑鼠右鍵按一下物件，然後選取 [**轉換架構**]。  
  
        物件轉換後，在 [存取中繼資料 Explorer] 中會顯示為粗體。  
  
    -   若要在一個步驟中轉換、載入和遷移架構和資料，請以滑鼠右鍵按一下 [資料庫]，然後選取 [**轉換]、[載入] 和 [遷移**]。  
  
4.  查看 [**輸出**] 窗格中的訊息，以及 [**錯誤清單**] 窗格中的任何錯誤和警告。  
  
## <a name="altering-tables-and-indexes"></a>改變數據表和索引  
在您將存取中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]轉換為或 sql azure 中繼資料，並將物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 之前，您可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]改變或 sql azure 資料表和索引。  
  
**若要改變數據表或索引屬性**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料瀏覽器中，選取您想要變更的資料表或索引。  
  
2.  在 [**資料表**] 索引標籤上，按一下您要修改的屬性，然後輸入或選取新的設定。 例如，您可以將 Nvarchar （15）變更為 Nvarchar （20），或選取核取方塊讓資料表資料行變成可為 null。  
  
    將游標移出 [已變更] 屬性儲存格。 若要這麼做，您可以按一下另一個資料列或按 Tab 鍵。  
  
3.  按一下 [套用]  。  
  
您現在可以在 [ **SQL** ] 索引標籤上，查看程式碼中的變更。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將[資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
