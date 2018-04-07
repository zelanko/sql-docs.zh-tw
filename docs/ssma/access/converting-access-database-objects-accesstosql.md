---
title: 轉換存取資料庫物件 (AccessToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
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
ms.workload: Inactive
ms.openlocfilehash: c05d0dd92d0802260f59f86fef13e617f6eea899
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="converting-access-database-objects-accesstosql"></a>轉換 (AccessToSQL) 來存取資料庫物件
您已加入 Access 資料庫，並連接到之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure、 SSMA 顯示中繼資料存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件。 您可以現在選取 存取資料庫物件，然後再轉換成結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 結構描述。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件會從存取中繼資料的物件定義、 將它們轉換為對等項目[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，並再將這項資訊載入至專案。 然後，您可以檢視[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件和其屬性使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管。  
  
> [!IMPORTANT]  
> 轉換物件並不會建立在物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 只將轉換的物件定義，並將資訊儲存在 SSMA 專案。  
  
在轉換期間，SSMA 會列印到輸出 窗格中，以及錯誤、 警告和錯誤清單 窗格來參考用訊息的狀態。 您可以使用此資訊來判斷是否需要修改您的 Access 資料庫或您的轉換程序，以取得所需的轉換結果。 您也可以使用中的資訊[準備移轉的 Access 資料庫](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)主題來判斷什麼會並不會進行轉換。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，請檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用此對話方塊中，您可以設定如何 SSMA 轉換索引備忘資料行、 主索引鍵、 外部索引鍵條件約束、 時間戳記和無索引的資料表。 如需詳細資訊，請參閱[專案設定 （轉換）](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示存取物件的轉換，以及產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件：  
  
|存取物件|產生的 SQL Server 物件|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|索引|索引|  
|外部索引鍵 (foreign key)|外部索引鍵 (foreign key)|  
|查詢|檢視<br /><br />大部份的 SELECT 查詢會轉換至檢視。 其他查詢，例如更新查詢，不會移轉。<br /><br />選取會採用參數的查詢不會轉換，也不是交叉分析查詢。|  
|報表|不會轉換|  
|表單|不會轉換|  
|macro|不會轉換|  
|module|不會轉換|  
|預設值|預設值|  
|允許在零長度資料行屬性|檢查條件約束|  
|資料行的驗證規則|檢查條件約束|  
|資料表驗證規則|檢查條件約束|  
|主索引鍵 (primary key)|主索引鍵 (primary key)|  
  
## <a name="converting-access-objects"></a>轉換存取物件  
若要轉換來存取資料庫物件，您必須先選取您想要轉換，然後再進行轉換的 SSMA 的物件。 若要進行轉換時，檢視輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**選取並將存取資料庫物件轉換成 SQL Server 或 SQL Azure 的語法**  
  
1.  在存取中繼資料總管，依序展開**存取 metabase**，然後展開**資料庫**。  
  
2.  請進行下列任一或多項操作：  
  
    -   若要轉換的所有資料庫，選取核取方塊旁的 **資料庫**。  
  
    -   若要轉換或省略個別資料庫，選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   轉換或省略查詢中，展開資料庫，然後選取或清除**查詢**核取方塊。  
  
    -   若要轉換或省略個別資料表中，展開資料庫，展開 **資料表**，然後選取或清除資料表旁的核取方塊。  
  
3.  執行下列其中之一：  
  
    -   若要轉換的結構描述，以滑鼠右鍵按一下**資料庫**選取**轉換結構描述**。  
  
        您也可以轉換個別物件。 要轉換的物件，無論哪個選取物件，以滑鼠右鍵按一下物件，並選取**轉換結構描述**。  
  
        當已轉換的物件時，它會出現粗體顯示在存取中繼資料總管。  
  
    -   若要轉換、 載入及移轉結構描述和資料在一個步驟中的，以滑鼠右鍵按一下資料庫，然後選取**轉換、 載入和移轉**。  
  
4.  檢視中的郵件**輸出**窗格及任何中錯誤和警告**錯誤清單**窗格。  
  
## <a name="altering-tables-and-indexes"></a>改變資料表和索引  
將存取中繼資料，以轉換之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料，以及物件載入之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您可以改變[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表和索引。  
  
**若要改變資料表或索引的屬性**  
  
1.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，選取您想要變更的索引的資料表。  
  
2.  在**資料表**索引標籤上，按一下您想要改變然後輸入或選取新設定的屬性。 比方說，您可以變更 nvarchar （20）、 nvarchar （15），或選取核取方塊，以便資料表資料行可為 null。  
  
    將游標移出已變更的屬性資料格中。 您可以按一下另一個資料列，或按下 Tab 鍵。  
  
3.  按一下 **[套用]**。  
  
您現在可以檢視變更的程式碼上**SQL**  索引標籤。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[轉換之資料庫的物件載入 SQL Server](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
