---
title: 轉換 Access 資料庫物件 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3db879598974e798c91fc274c0c2dff0d2205358
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392736"
---
# <a name="converting-access-database-objects-accesstosql"></a>轉換 Access 資料庫物件 (AccessToSQL)
在您加入 Access 資料庫並連接到後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure、 SSMA 顯示中繼資料存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫物件。 您可以現在選取 存取的資料庫物件，然後將轉換將結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 結構描述。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件會從存取中繼資料的物件定義、 將它們轉換為對等項目[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，然後將 載入專案的 這項資訊。 然後，您可以檢視[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件和其屬性使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管。  
  
> [!IMPORTANT]  
> 將物件轉換不會建立在物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 只將物件定義轉換，並將資訊儲存在 SSMA 專案。  
  
在轉換期間 SSMA 會列印到輸出 窗格中，以及錯誤、 警告和錯誤清單 窗格來參考用訊息的狀態。 您可以使用此資訊來判斷是否需要修改您的 Access 資料庫或您的轉換程序，以便取得所需的轉換結果。 您也可以使用中的資訊[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)主題，以判斷將並不會轉換。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用這個對話方塊中，您可以設定如何 SSMA 轉換索引備忘資料行、 主索引鍵、 外部索引鍵條件約束、 時間戳記和無索引的資料表。 如需詳細資訊，請參閱[專案設定 （轉換）](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示可存取物件的轉換，並產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件：  
  
|存取物件|產生的 SQL Server 物件|  
|-----------------|-------------------------------|  
|資料表|資料表|  
|column|column|  
|索引|索引|  
|外部索引鍵 (foreign key)|外部索引鍵 (foreign key)|  
|查詢|檢視<br /><br />大部份的 SELECT 查詢會轉換成檢視。 其他查詢，例如更新查詢，不會移轉。<br /><br />採用參數的 SELECT 查詢不會轉換，也不會交叉分析查詢。|  
|報表|未轉換|  
|表單|未轉換|  
|巨集|未轉換|  
|module|未轉換|  
|預設值|預設值|  
|允許在零長度資料行屬性|檢查條件約束|  
|資料行的驗證規則|檢查條件約束|  
|資料表驗證規則|檢查條件約束|  
|主索引鍵 (primary key)|主索引鍵 (primary key)|  
  
## <a name="converting-access-objects"></a>轉換存取物件  
若要轉換 Access 資料庫物件，您必須先選取您想要轉換，然後再執行轉換的 SSMA 的物件。 若要檢視轉換期間的輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要選取，然後將 Access 資料庫物件轉換成 SQL Server 或 SQL Azure 的語法**  
  
1.  在存取中繼資料總管 中，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要將所有的資料庫轉換，選取核取方塊旁**資料庫**。  
  
    -   若要將轉換或省略個別資料庫，選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   要轉換，或省略查詢，請展開資料庫，然後選取或清除**查詢**核取方塊。  
  
    -   若要轉換，或省略個別資料表，展開資料庫，依序展開**資料表**，然後選取或清除資料表旁邊的核取方塊。  
  
3.  執行下列其中之一：  
  
    -   若要將結構描述的轉換，以滑鼠右鍵按一下**資料庫**，然後選取**轉換的結構描述**。  
  
        您也可以將個別的物件。 若要轉換的物件，不論所選取物件，以滑鼠右鍵按一下物件，然後選取**轉換的結構描述**。  
  
        當已轉換的物件時，它會出現粗體存取中繼資料總管 中。  
  
    -   若要將轉換、 載入及移轉結構描述和資料在一個步驟中的，以滑鼠右鍵按一下資料庫，然後選取**轉換、 載入和移轉**。  
  
4.  檢閱中的訊息**輸出** 窗格和所有中錯誤和警告**錯誤清單**窗格。  
  
## <a name="altering-tables-and-indexes"></a>改變資料表及索引  
在轉換到存取中繼資料之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料，以及之前載入至物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您可以變更[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表和索引。  
  
**若要改變資料表或索引的屬性**  
  
1.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管]，選取您想要改變的索引的資料表。  
  
2.  在 **資料表**索引標籤上，按一下您想要改變然後輸入或選取新設定的屬性。 例如，您可以將 nvarchar(15) 變更 nvarchar(20)，，或選取核取方塊，將資料表資料行可為 null。  
  
    將游標移出已變更的屬性資料格中。 您可以按一下另一個資料列，或按下 Tab 鍵來這樣做。  
  
3.  按一下 **[套用]**。  
  
您現在可以在檢視中的程式碼的變更**SQL**  索引標籤。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[轉換之資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
