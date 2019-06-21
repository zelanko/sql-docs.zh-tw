---
title: 不相容的 Access 功能 (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 29b5225f95c6b2cb04f42c0e67c504ac2cb20e53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740893"
---
# <a name="incompatible-access-features-accesstosql"></a>不相容的 Access 功能 (AccessToSQL)
並非所有的 Access 資料庫功能都相容於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 比方說，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和存取有不同的保留關鍵字。 問題，例如這些妨礙成功移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以使用下表來深入了解可能的移轉問題，以及您可以執行其相關。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>資料庫設定] 或 [可能會影響移轉的功能  
  
|存取資料庫的設定或功能|移轉問題|  
|--------------------------------------|-------------------|  
|存取資料表沒有唯一索引。|如果沒有唯一索引的資料表移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您無法在移轉後修改資料表。 這可能會導致應用程式相容性問題。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出任何存取資料表沒有唯一索引。<br /><br />您可以設定上新增主索引鍵存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]轉換期間的資料表。 如需詳細資訊，請參閱 <<c0> [ 專案設定 （轉換）](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)。|  
|存取資料表有複寫的資料行。|如果要將 Access 資料表包含複寫系統的資料行移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Jet 複寫功能在移轉之後將會中斷。<br /><br />移轉之後，請考慮使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來維護您的資料庫已同步處理的複本的複寫。|  
|具有唯一索引的 access 資料表包含多個 null 值。|存取資料表，具有多個 null 值的唯一索引不得轉移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，因為在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，唯一的索引不允許多個 null 值。 移轉這些資料表將會失敗。<br /><br />SSMA 會加上旗標的評估報告這個問題。 若要建立的評估報告，請參閱[評定 Access 資料庫物件進行轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />如果此問題存在，您必須確定主索引鍵沒有重複的 null 值。 或者，您必須移除主索引鍵或唯一包含多個 null 值的索引。|  
|存取資料表包含的日期值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範圍。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime**類型接受範圍內以 31 年 12 月的 1 年 1 月 1753年的日期只有 9999。 存取接受 31 年 12 月 1 年 1 月 100年的範圍內的日期到 9999。<br /><br />SSMA 會加上旗標的評估報告這個問題。 若要建立的評估報告，請參閱[評定 Access 資料庫物件進行轉換](assessing-access-database-objects-for-conversion-accesstosql.md)。<br /><br />您可以設定 SSMA 如何解決日期所共[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範圍。 如需詳細資訊，請參閱 <<c0> [ 專案設定 （移轉）](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)。|  
|索引長度，以存取超過 900 個位元組。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引具有索引鍵資料行的大小總計 900 位元組限制。 如果您的 Access 資料表會使用較大的索引，SSMA 會顯示警告。<br /><br />如果您繼續進行資料移轉，移轉可能會失敗。|  
|存取物件的名稱都[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]關鍵字，或包含特殊字元。|存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有不同的保留的關鍵字和特殊字元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接受物件的命名方式是使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]關鍵字，或請如果您使用方括號識別碼或引號識別碼，例如 「 select 」，或 [選取].p 包含特殊字元。 如需詳細資訊，請參閱 < 分隔識別碼 (Database Engine) > 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。<br /><br />**注意：** 若要使用引號分隔識別碼，SET QUOTED_IDENTIFIER 必須是 ON。<br /><br />比方說，`CREATE TABLE [schema](c1 [FOR])`是有效的陳述式，即使**結構描述**並**如**是保留的關鍵字。 此外，`CREATE TABLE [xxx*yyy](c1 x&y)`是有效的陳述式，即使資料表和資料行名稱包含特殊字元 **\&#42;** 並 **&amp;** 。<br /><br />所有的查詢會參考這些物件也必須使用名稱使用方括號或引號。 例如，查詢`SELECT * FROM schema`將會失敗。 正確的查詢是： `SELECT * FROM [schema]`。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 窗格會列出使用的關鍵字或特殊字元的任何存取資料表。 您可以修改在 Access 中，資料表和移除並再次; 新增資料庫或者，您可以修改，讓查詢使用方括號或引號來分隔識別碼參考這些物件的查詢。 如果您不會修改您的查詢，存取應用程式可能會傳回錯誤，或有其他問題。|  
|欄位大小的差異在於主索引鍵/外部索引鍵關聯性。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援連結具有不同的資料類型或使用 foreign key 條件約束的大小的資料行的 Jet 功能。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出任何主索引鍵/外部索引鍵條件約束不會轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以變更資料類型和存取資料行的大小，讓它們符合，然後移除並重新加入 Access 資料庫。 或者，您可以移轉資料，雖然這些條件約束不會建立在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|存取關聯性中參考的資料表沒有主索引鍵也沒有唯一索引。|存取會接受其中參考的資料表沒有主索引鍵或唯一索引的資料表之間的關聯性。 不過，這不支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />當您轉換 Access 資料庫物件時，[輸出] 視窗會列出任何關聯性，但沒有主索引鍵或唯一索引的資料表。 您可以變更要將主索引鍵或唯一索引，然後移除並重新加入 Access 資料庫的資料表。 或者，您可以移轉資料，雖然資料表之間的關聯性將會中斷。|  
|存取資料表有超連結資料行。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援**超連結**資料行。 相反地，資料行被視為存取備忘資料行。 根據預設，將這些資料行轉換成**nvarchar （max)** 中的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以自訂對應。 如需詳細資訊，請參閱 <<c0> [ 對應來源和目標資料型別](mapping-source-and-target-data-types-accesstosql.md)。|  
|預設值或驗證規則運算式包含無法轉換成的存取函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。|存取預設運算式或驗證規則可能包括存取系統函數或使用者定義的函式，不會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 使用不會對應至的函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 會防止載入預設運算式或驗證規則，到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。|  
  
## <a name="see-also"></a>另請參閱  
[準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
