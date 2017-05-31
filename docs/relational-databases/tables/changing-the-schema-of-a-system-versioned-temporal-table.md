---
title: "變更系統設定版本時態表的結構描述 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97eadf63fb8332ef55d8ccb699241a5e5f0e19d0
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>變更系統建立版本時態表的結構描述
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用 **ALTER TABLE** 陳述式加入、改變或移除資料行。  
  
## <a name="examples"></a>範例  
 以下是變更時態表結構描述的一些範例。  
  
```  
ALTER TABLE dbo.Department   
   ALTER COLUMN  DeptName varchar(100);   
  
ALTER TABLE dbo.Department   
   ADD WebAddress nvarchar(255) NOT NULL    
   CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';   
  
ALTER TABLE dbo.Department   
   ADD TempColumn INT;   
  
GO   
  
ALTER TABLE dbo.Department   
   DROP COLUMN TempColumn;  
  
/* Setting IsHidden property for period columns.   
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */  
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysStartTime ADD HIDDEN;   
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysEndTime ADD HIDDEN;  
  
```  
  
### <a name="important-remarks"></a>重要備註  
  
-   變更時態表結構描述所需的目前和記錄資料表的**CONTROL** 權限。  
  
-   在 **ALTER TABLE** 作業期間，系統會保留這兩個資料表的結構描述鎖定。  
  
-   指定的結構描述變更會以適當的方式 (視變更的類型而定) 傳播至記錄資料表  
  
-   如果您加入不可為 Null 資料行，或改變現有資料行使其成為不可為 Null，則必須指定現有資料列的預設值。 系統會產生具有相同值的其他預設值，並將它套用到記錄資料表。 將 **DEFAULT** 加入非空白資料表，是所有版本的資料作業大小 (為中繼資料作業的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 除外)。  
  
-   加入 varchar(max)、nvarchar(max)、varbinary(max) 或含有預設值的 XML 資料行，將是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的更新資料作業。  
  
-   如果加入資料行之後的資料列大小超過資料列大小限制，則無法線上加入新的資料行。  
  
-   使用新的 NOT NULL 資料行擴充資料表之後，請考慮卸除記錄資料表的預設條件約束，因為系統會自動填入該資料表中的所有資料行。  
  
-   若為系統版本設定時態表，ONLINE 選項 (**WITH (ONLINE = ON**) 對 **ALTER TABLE ALTER COLUMN** 無效。 無論針對 ONLINE 選項指定何值，皆不會將 ALTER 資料行執行為線上。  
  
-   您可以使用 **ALTER COLUMN** 變更期間資料行的 **IsHidden** 屬性。  
  
-   您不能使用直接 **ALTER** 進行下列結構描述變更。 針對這些類型的變更，請設定 **SYSTEM_VERSIONING = OFF**。  
  
    -   加入計算資料行  
  
    -   加入 **IDENTITY** 資料行  
  
    -   在記錄資料表設定為 **DATA_COMPRESSION = PAGE** 或 **DATA_COMPRESSION = ROW**(記錄資料表的預設值) 時加入 **SPARSE** 資料行或將現有資料行變更為 **SPARSE**。  
  
    -   加入 **COLUMN_SET**  
  
    -   加入 **ROWGUIDCOL** 資料行或將現有資料行變更為 **ROWGUIDCOL**  
  
         下列範例示範如何變更仍需要設定 **SYSTEM_VERSIONING = OFF** 的結構描述 (加入 **IDENTITY** 資料行)。   
        請注意，此範例會停用資料一致性檢查。 因為不能發生任何並行資料變更，所以在交易內進行結構描述變更時不需要這項檢查。  
  
        ```  
        BEGIN TRAN   
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);   
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);   
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;   
        ALTER TABLE [dbo].[CompanyLocation]    
        SET    
        (   
        SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[CompanyLocationHistory])   
        );   
        COMMIT ;  
  
        ```  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Changing%20the%20Schema%20of%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>另請參閱  
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [建立系統建立版本的時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [停止系統版本設定時態表上的系統版本設定功能](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  

