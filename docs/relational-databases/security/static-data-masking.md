---
title: 靜態資料遮罩 | Microsoft Docs
ms.date: 11/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: egranet
ms.author: aliceku
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cec6c79fadb5ef2a63145fff3efe0df3c8cd0f9d
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980454"
---
# <a name="static-data-masking"></a>靜態資料遮罩
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

靜態資料遮罩是 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 Preview 5 和更新版本的元件。 您可以在[這裡](../../ssms/download-sql-server-management-studio-ssms.md)下載 SQL Server Management Studio 的最新預覽版。 

![靜態資料遮罩](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>什麼是靜態資料遮罩？ 
靜態資料遮罩是 SQL Server Management Studio 的一項功能，可讓使用者建立資料庫的遮罩複本。 這項功能是專為需要在小組之間或與其他組織共用資料 (其中一部分為敏感性) 的組織所開發。 

靜態資料遮罩藉由將敏感性資料 (遮罩前資料) 取代為新資料 (遮罩後資料) 來協助進行下列情節： 
- 開發和測試 
- 分析和商務報告 
- 疑難排解 
- 與顧問、研究小組或任何第三方共用資料庫 

下列範例示範靜態資料遮罩的實際運作方式。 遮罩前，資料行包含社會安全號碼。 遮罩後，每個社會安全號碼前五位數已取代為隨機產生的數字。

| 美國社會安全號碼 (遮罩前)   | 美國社會安全號碼 (遮罩後)  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

靜態資料遮罩的使用者可以從數項遮罩功能中進行選擇。 根據遮罩功能，遮罩前資料與遮罩後資料可能高度相關或完全無關。 執行隨機顯示的遮罩功能會使遮罩後資料與遮罩前資料維持高度相關。 

| 美國社會安全號碼 (遮罩前) | 美國社會安全號碼 (遮罩後) |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

執行以 NULL 值取代的遮罩功能會使遮罩後資料與遮罩前資料維持無關。 
 
| 美國社會安全號碼 (遮罩前) | 美國社會安全號碼 (遮罩後) |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>靜態資料遮罩的運作方式
靜態資料遮罩會在資料行層級進行。 使用者可以選取想要遮罩的資料行，並針對每個所選資料行選取想要套用的遮罩功能。 有數個遮罩功能可供您選擇。 [遮罩功能](#masking-functions)中將詳細描述這些功能。 

靜態資料遮罩接著會建立資料庫複本。 針對 Azure SQL Database，則會透過[複製功能](https://azure.microsoft.com/blog/static-data-masking-preview/)來執行此複本。 針對 SQL Server，則會透過備份作業並接著還原作業來執行此複本。 由此，針對每個資料行，靜態資料遮罩會開始根據所選取的遮罩功能，將遮罩前資料取代為遮罩後資料。 

取代是在儲存體層級完成。 因此，靜態資料遮罩完成之後，您將無法從資料庫的遮罩複本擷取遮罩前資料。

## <a name="how-to-guide"></a>操作指南

以下是執行靜態資料遮罩的逐步指南。 
 
1. 啟動 SQL Server Management Studio。 連線到您的資料庫。 在左側的 [物件總管] 窗格中，展開 [資料庫] 資料夾。 以滑鼠右鍵按一下您想要遮罩的資料庫。 按一下 [工作]。 以滑鼠左鍵按一下 [遮罩資料庫...(預覽)]。
 
 ![[工作] 功能表](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. 遮罩設定視窗隨即快顯。 它會顯示資料庫中的所有資料表。 資料表是由結構描述所顯示，然後依結構描述中的字母順序排序。 
 
 ![使用者介面](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. 按一下資料表名稱旁的下拉式清單圖示，以取得資料表中的所有資料行清單。 針對資料表中的每個資料行，系統會指定資料行的資料類型，以及資料行是否可為 Null。 可為 Null 的資料行是可接收 NULL 值作為輸入的資料行。 
 
 ![資料表下拉式清單](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. 選取您想要遮罩的所有資料行，以及您想要套用的遮罩功能。 可用的遮罩類型包括 [隨機顯示] 遮罩、[Group Shuffle] \(群組隨機顯示\) 遮罩、[單一值] 遮罩、[NULL] 遮罩、[String Composite] \(字串複合\) 遮罩。 
 
 ![遮罩功能下拉式清單](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 附註：大多數遮罩功能會有其他設定參數。 針對 [隨機顯示] 遮罩，靜態資料遮罩會提供預設參數。 針對 [Group Shuffle] \(群組隨機顯示\) 遮罩、[單一值] 遮罩和 [String Composite] \(字串複合\) 遮罩，使用者必須提供設定參數。 若要變更或提供設定參數，請按一下 [設定] 選項，然後在快顯對話方塊中指定參數的 (替代) 值。 [遮罩功能](#masking-functions)中提供每項遮罩功能的詳細說明。
 
 ![遮罩功能設定按鈕](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 遮罩設定選項會即時驗證是否有設定和結構描述相關錯誤和警告。  任何偵測到的錯誤和警告都會在左邊顯示為一個圖示，您可將滑鼠游標移至上方以取得其他詳細資料。 
 
 在下列範例中，使用者針對不允許 NULL 值 (非 NULL 條件約束) 的資料行選取了 [NULL] 遮罩。
 
 ![驗證機制錯誤](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 在下列範例中，使用者只針對一個資料行選取 [Group Shuffle] \(群組隨機顯示\) 遮罩。 由於 [Group Shuffle] \(群組隨機顯示\) 遮罩需要至少兩個資料行，因此已發出警告。 
 
 ![驗證機制警告](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. 您可將完成的遮罩設定儲存至 XML 檔案，以供稍後使用。  雖然 Azure SQL Database 的遮罩功能設定與內部部署資料庫完全相同，但有些微差異，那就是會儲存其他屬性 (例如備份檔案路徑)。 若要儲存設定，請按一下 [Save Config] \(儲存設定\)，提供檔案名稱，然後按一下 [儲存]。  使用者稍後可以使用 [Load Config] \(載入設定\) 載入現有的設定檔。建議針對具有大量資料行的資料表使用設定檔。 
 
 ![組態檔](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. 靜態資料遮罩會在使用者的 [文件] 資料夾中，建立名為「靜態資料遮罩」的資料夾，並將記錄檔置於其中。 記錄檔可協助進行偵錯。 設定視窗底部會指出記錄檔的名稱。 
  
 
7. (僅限 SQL Server) 如果您在內部部署資料庫上執行靜態資料遮罩，靜態資料遮罩會執行備份/還原作業。 在 [Step 2: Clone .BAK file Location] \(步驟 2：複製 .BAK 檔案位置\) 中，提供要在伺服器上儲存備份檔案的位置。 

## <a name="masking-functions"></a>遮罩功能

### <a name="null-masking"></a>[NULL] 遮罩

[NULL] 遮罩會將資料行中的所有值取代為 NULL。 如果資料行不允許 NULL 值，則 靜態資料遮罩工具會傳回錯誤。 

### <a name="single-value-masking"></a>[單一值] 遮罩

[單一值] 遮罩會將資料行中的所有值取代為單一固定值，此值是由使用者指定。 輸入格式必須可轉換成所選資料行的任何類型。 若要指定值，請按一下 [設定] 並提供值，然後按一下 [確定]。 

![[單一值] 遮罩參數](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>[隨機顯示] 遮罩

資料行中的所有值會隨機顯示於新資料列。 不會產生新資料。 [隨機顯示] 遮罩可讓您選擇保留資料行中的 NULL 項目。 若要這樣做，請按一下 [設定...]，然後選取 [Maintain NULL positions] \(保留 NULL 位置\) 方塊。

![[隨機顯示] 遮罩參數](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

以下是 [隨機顯示] 遮罩範例，其 NULL 值從不就地保留變成就地保留。


| 美國社會安全號碼 (遮罩前) | 美國社會安全號碼 (遮罩後並隨機顯示 NULL 項目) | 美國社會安全號碼 (遮罩後但不隨機顯示 NULL 項目) |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>[Group Shuffle] \(群組隨機顯示\) 遮罩
[Group Shuffle] \(群組隨機顯示\) 會將數個資料行繫結成一個隨機顯示群組。 隨機顯示群組中的資料行會一起隨機顯示。 使用者必須使用 [設定...] 選項來指定隨機顯示群組的名稱。

![[Group Shuffle] \(群組隨機顯示\) 遮罩參數](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

群組隨機顯示發生於相同資料表中；如果多個資料表中使用了相同的隨機顯示群組名稱，則兩個群組隨機顯示為獨立動作。 群組名稱必須相同，才能在群組中包含每個資料行。 名稱會區分大小寫。 多個隨機顯示群組 (具有不同名稱) 可發生於相同的資料表中。 

### <a name="string-composite-masking"></a>[String Composite] \(字串複合\) 遮罩

[String Composite] \(字串複合\) 遮罩會依某個模式產生隨機字串。 它是專為必須遵循預先定義模式才是有效項目的字串所設計。 例如，美國社會安全號碼的格式為 123-45-6789。 [String Composite] \(字串複合\) 遮罩的語法是在對話方塊中指定，使用者必須在其中輸入模式。

![[String Composite] \(字串複合\) 遮罩參數](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

[String Composite] \(字串複合\) 遮罩提供三個範例模式，可在其上按一下來進行測試。 如果您按一下 [電話號碼]，模式方塊會自動填入產生隨機美國電話號碼所需的公式。

![[String Composite] \(字串複合\) 遮罩參數範例](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

[String Composite] \(字串複合\) 遮罩還有進階模式，允許以模式所產生字串來取代現有資料的子區段。 所取代字串部分取決於規則運算式中的擷取群組。 例如，電子郵件的使用者名稱部分可在保留網域的情況下加以取代，或是電話號碼可透過保留區碼來取代。 如需規則運算式的詳細資訊，請參閱[這裡](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference)。

![進階 [String Composite] \(字串複合\) 遮罩參數範例](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

[String Composite] \(字串複合\) 遮罩及其進階模式只能用於[資料類型](../../t-sql/data-types/data-types-transact-sql.md)為 char、varchar、text、nchar、nvarchar、ntext 的資料行。

## <a name="limitations"></a>限制 

靜態資料遮罩具有下列限制：

- 靜態資料遮罩不支援具有[時態表](../../relational-databases/tables/temporal-tables.md)的資料庫。

- 靜態資料遮罩不會遮罩[經記憶體最佳化](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)的資料表。

- 靜態資料遮罩不會遮罩[計算資料行](../../relational-databases/tables/specify-computed-columns-in-a-table.md)和[識別](../../t-sql/statements/create-table-transact-sql-identity-property.md)欄位。

- 靜態資料遮罩不支援 Azure SQL 超大規模資料庫。

- 靜態資料遮罩不支援幾何與地理資料類型。 

此外，靜態資料遮罩在其遮罩功能方面有三項限制：

- 靜態資料遮罩無法更新[長條圖統計資料](../../relational-databases/statistics/statistics.md)。 因此，完成靜態資料遮罩之後，資料庫的遮罩複本可能仍會包含長條圖統計資料中的敏感性資料。 請考慮執行 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) 以修正此問題。 

- 如果靜態資料遮罩傳回錯誤，則會暫止所有遮罩作業。 資料庫複本不會被刪除，因此可能包含敏感性資訊。 如果靜態資料遮罩傳回錯誤，使用者會負責刪除資料庫複本。 

- (僅限 SQL Server) 在靜態資料遮罩完成之後，[資料檔案](../../relational-databases/databases/database-files-and-filegroups.md)和[記錄檔](../../relational-databases/logs/the-transaction-log-sql-server.md)可能仍會在未配置的記憶體中包含一些敏感性資料。 如果授與資料檔案和記錄檔的存取權，則可以使用十六進位編輯器擷取此敏感性資料。

## <a name="see-also"></a>另請參閱  
 [動態資料遮罩](../../relational-databases/security/dynamic-data-masking.md)   
 [開始使用 SQL Database 靜態資料遮罩](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
