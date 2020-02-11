---
title: 不相容的存取功能（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2cc48fa530730beec07aaca4bfb933c9ff8fb2b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986352"
---
# <a name="incompatible-access-features-accesstosql"></a>不相容的存取功能（AccessToSQL）
並非所有 Access 資料庫功能都與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相容。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 Access 有不同組的保留關鍵字。 這些問題可能會導致無法成功地遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請使用下表來瞭解可能的遷移問題，以及您可以對其採取哪些動作。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>可能會影響遷移的資料庫設定或功能  
  
|Access 資料庫設定或功能|遷移問題|  
|--------------------------------------|-------------------|  
|Access 資料表沒有唯一的索引。|如果沒有唯一索引的資料表已遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您就無法在遷移之後修改資料表。 這可能會導致應用程式相容性問題。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出任何沒有唯一索引的 Access 資料表。<br /><br />您可以設定在轉換期間將主鍵加入資料表的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存取權。 如需詳細資訊，請參閱[專案設定（轉換）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)。|  
|Access 資料表具有複寫資料行。|如果包含複寫系統資料行的 Access 資料表已遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則 Jet 複寫功能會在遷移之後中斷。<br /><br />遷移之後，請考慮[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用複寫來維護資料庫的同步複本。|  
|具有唯一索引的存取資料表包含多個 null 值。|具有多個 null 值之唯一索引的存取資料表無法轉移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因為在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，唯一索引不允許多個 null。 這些資料表的遷移將會失敗。<br /><br />SSMA 會在評估報告中加上此問題的旗標。 若要建立評量報告，請參閱[評定 Access 資料庫物件的轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />如果這個問題存在，您必須確定主鍵沒有重複的 null 值。 或者，您必須移除包含多個 null 值的主鍵或唯一索引。|  
|Access 資料表包含超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範圍的日期值。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **日期時間**類型只接受介於 1 Jan 1753 到 31 Dec 9999 之間的日期。 存取會接受介於 1 Jan 100 到 31 Dec 9999 之間的日期。<br /><br />SSMA 會在評估報告中加上此問題的旗標。 若要建立評量報告，請參閱[評定 Access 資料庫物件的轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />您可以設定 SSMA 如何解析超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範圍的日期。 如需詳細資訊，請參閱[專案設定（遷移）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。|  
|存取中的索引長度超過900個位元組。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]索引索引鍵資料行的總大小有900個位元組的限制。 如果您的 Access 資料表使用較大的索引，SSMA 會顯示警告。<br /><br />如果您繼續進行資料移轉，則遷移可能會失敗。|  
|存取物件名稱是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]關鍵字，或包含特殊字元。|存取並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擁有不同的保留關鍵字組和特殊字元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您使用括弧或引號識別碼（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]例如 "select" 或 [select]. p），則會接受使用關鍵字或包含特殊字元的物件。 如需詳細資訊，請參閱《線上叢書》中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的「分隔識別碼（資料庫引擎）」。<br /><br />**注意：** 若要使用引號分隔識別碼，SET QUOTED_IDENTIFIER 必須是 ON。<br /><br />例如， `CREATE TABLE [schema](c1 [FOR])`是有效的語句，即使**架構**和是保留**關鍵字也是**一樣。 此外， `CREATE TABLE [xxx*yyy](c1 x&y)`雖然資料表和資料行名稱包含特殊字元** \&#42** ，但也是有效的語句。 **&amp;**<br /><br />所有參考這些物件的查詢，也必須使用以方括弧或引號括住的名稱。 例如，查詢`SELECT * FROM schema`將會失敗。 正確的查詢為： `SELECT * FROM [schema]`。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 窗格會列出任何使用關鍵字或特殊字元的 Access 資料表。 您可以修改 Access 中的資料表，然後再次移除並加入資料庫。或者，您可以修改參考這些物件的查詢，讓查詢使用括弧或引號來分隔識別碼。 如果您未修改查詢，您的存取應用程式可能會傳回錯誤或有其他問題。|  
|主鍵/外鍵關聯性中的欄位大小不同。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援連結具有外鍵條件約束之不同資料類型或大小之資料行的 Jet 功能。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗將會列出任何將不會轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的主鍵/外鍵條件約束。 您可以在存取資料行上修改資料類型和大小，使其符合，然後移除並重新加入 Access 資料庫。 或者，您可以遷移資料，但不會在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立這些條件約束。|  
|存取關聯性中的參考資料表不具有主鍵或唯一索引。|存取會接受參考資料表沒有主鍵或唯一索引之資料表之間的關聯性。 不過，不支援這種情況[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出任何具有關聯性但沒有主鍵或唯一索引的資料表。 您可以變更資料表來加入主鍵或唯一索引，然後移除並重新加入 Access 資料庫。 或者，您可以遷移資料，但資料表之間的關聯性將會中斷。|  
|Access 資料表具有超連結資料行。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支援**超連結**資料行。 相反地，會將資料行視為存取備忘資料行。 根據預設，這些資料行會轉換成中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Nvarchar （max）** 資料行。 您可以自訂對應。 如需詳細資訊，請參閱[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)。|  
|預設或驗證規則運算式包含無法轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的存取函數。|存取預設運算式或驗證規則可能包括未對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的 access 系統函數或使用者定義函數。 使用未對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 的函式，將會讓您無法將預設運算式或驗證規則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]載入或 sql azure 中。|  
  
## <a name="see-also"></a>另請參閱  
[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
