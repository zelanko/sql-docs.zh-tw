---
title: 不相容的存取功能 (AccessToSQL) |Microsoft Docs
description: 瞭解與 SQL Server 不相容之 Access 資料庫功能的可能遷移問題，以及如何解決這些問題。
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4ecf50e11bab0d6e1034299cba87c40137556505
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985132"
---
# <a name="incompatible-access-features-accesstosql"></a> (AccessToSQL) 不相容的存取功能
並非所有 Access 資料庫功能都與相容 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Access 具有不同組的保留關鍵字。 這些問題可能會導致無法成功地遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 使用下表來瞭解可能的遷移問題，以及您可以執行的動作。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>可能會影響遷移的資料庫設定或功能  
  
|存取資料庫設定或功能|遷移問題|  
|--------------------------------------|-------------------|  
|Access 資料表沒有唯一的索引。|如果沒有唯一索引的資料表遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您就無法在遷移之後修改資料表。 這可能會導致應用程式相容性問題。<br /><br />當您轉換 Access 資料庫物件時，輸出視窗會列出沒有唯一索引的任何存取資料表。<br /><br />您可以設定存取權，在轉換期間于資料表上加入主鍵 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱 [ (轉換) 的專案設定 ](./project-settings-conversion-accesstosql.md)。|  
|Access 資料表具有複寫資料行。|如果包含複寫系統資料行的存取資料表遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則在遷移之後，Jet 複製功能將會中斷。<br /><br />在遷移之後，請考慮使用複寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來維護資料庫的同步複本。|  
|存取具有唯一索引的資料表包含多個 null 值。|具有具有多個 null 值之唯一索引的存取資料表無法傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，因為在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，唯一索引不允許多個 null。 這些資料表的遷移將會失敗。<br /><br />SSMA 會在評量報告中標示此問題。 若要建立評量報告，請參閱 [評定 Access 資料庫物件的轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />如果有這個問題，您必須確定主鍵沒有重複的 null 值。 或者，您必須移除包含多個 null 值的 primary key 或 unique 索引。|  
|Access 資料表包含超出範圍的日期值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime**類型只接受1月1753到 31 Dec 9999 之間的日期。 存取會接受範圍介於1年1月100到 31 Dec 9999 之間的日期。<br /><br />SSMA 會在評量報告中標示此問題。 若要建立評量報告，請參閱 [評定 Access 資料庫物件的轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />您可以設定 SSMA 如何解析超出範圍的日期 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱 [ (遷移) 的專案設定 ](./project-settings-migration-accesstosql.md)。|  
|存取中的索引長度超過900個位元組。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引的索引鍵資料行大小總計有900個位元組的限制。 如果您的存取資料表使用較大的索引，SSMA 會顯示警告。<br /><br />如果您繼續進行資料移轉，則遷移可能會失敗。|  
|存取物件名稱是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關鍵字，或包含特殊字元。|存取並 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擁有不同組的保留關鍵字和特殊字元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果您使用括弧或引號的識別碼（例如 "select" 或 [select]. p），則會接受使用關鍵字所命名或包含特殊字元的物件。 如需詳細資訊，請參閱《線上叢書》中的「分隔識別碼 (資料庫引擎) 」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />**注意：** 若要使用引號分隔識別碼，請設定 QUOTED_IDENTIFIER 必須是 ON。<br /><br />例如， `CREATE TABLE [schema](c1 [FOR])` 是有效的語句，即使 **架構** 和 **FOR** 是保留關鍵字也是一樣。 此外，也 `CREATE TABLE [xxx*yyy](c1 x&y)` 是有效的語句，即使資料表和資料行名稱包含** \& #42**的特殊字元也是一樣 **&amp;** 。<br /><br />參考這些物件的所有查詢也必須使用括弧或引號括住的名稱。 例如，查詢 `SELECT * FROM schema` 將會失敗。 正確的查詢為： `SELECT * FROM [schema]` 。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 窗格會列出使用關鍵字或特殊字元的任何存取資料表。 您可以修改 Access 中的資料表，然後再次移除並加入資料庫。或者，您可以修改參考這些物件的查詢，讓查詢使用括弧或引號分隔識別碼。 如果您沒有修改查詢，您的存取應用程式可能會傳回錯誤或有其他問題。|  
|主鍵/外鍵關聯性中的欄位大小不同。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援連結具有不同資料類型的資料行或具有外鍵條件約束之大小的 Jet 功能。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗將會列出任何將不會轉換成的主鍵/外鍵條件約束 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以變更存取資料行的資料類型和大小，使其相符，然後再移除並重新加入 Access 資料庫。 或者，您可以遷移資料，不過這些條件約束將不會建立在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|存取關聯性中參考的資料表不具有主鍵或唯一索引。|存取接受資料表之間的關聯性，其中參考的資料表沒有主鍵或唯一索引。 但是，不支援這項功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出具有關聯性但沒有主鍵或唯一索引的任何資料表。 您可以改變數據表來加入主鍵或唯一索引，然後移除並重新加入 Access 資料庫。 或者，您可以遷移資料，雖然資料表之間的關聯性將會中斷。|  
|Access 資料表有超連結資料行。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 **超連結** 資料行。 取而代之的是，資料行的處理方式就像存取備忘錄資料行一樣。 根據預設，這些資料行會轉換成中的 **Nvarchar (max) ** 資料行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以自訂對應。 如需詳細資訊，請參閱 [對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)。|  
|預設或驗證規則運算式包含無法轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 的存取功能。|存取預設運算式或驗證規則可能包括存取系統函數或未對應至 SQL Azure 的使用者定義函數 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 使用未對應至或 SQL Azure 的函式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會讓您無法將預設運算式或驗證規則載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure。|  
  
## <a name="see-also"></a>另請參閱  
[準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
