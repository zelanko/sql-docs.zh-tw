---
title: "不相容的存取功能 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "18"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59c6c7d0130c93efb7e5d3136deb0edbd5d05ab9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="incompatible-access-features-accesstosql"></a>不相容的存取功能 (AccessToSQL)
並非所有存取資料庫的功能都都相容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和存取具有不同的保留關鍵字集合。 問題如這些可以阻礙成功移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 若要了解可能的移轉問題，您可以執行資訊，請使用下表。  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>資料庫的設定或可能會影響移轉的功能  
  
|存取資料庫的設定或功能|移轉問題|  
|--------------------------------------|-------------------|  
|存取資料表沒有唯一索引。|如果沒有唯一索引的資料表移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您無法在移轉後修改資料表。 這可能會導致應用程式相容性問題。<br /><br />當您轉換來存取資料庫物件時，[輸出] 視窗會列出任何存取資料表沒有唯一索引。<br /><br />您可以設定的存取權加入主索引鍵上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]轉換期間的資料表。 如需詳細資訊，請參閱[（轉換） 的專案設定](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)。|  
|存取資料表有複寫的資料行。|如果要將包含複寫系統的資料行的存取資料表移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，移轉之後，Jet 複寫功能將會中斷。<br /><br />移轉之後，請考慮使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]維護資料庫已同步處理的複本的複寫。|  
|存取資料表的唯一索引包含多個 null 值。|存取資料表具有多個 null 值的唯一索引的無法傳送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，因為在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，唯一的索引不允許多個 null 值。 移轉這些資料表將會失敗。<br /><br />SSMA 會加上旗標評估報告這個的問題。 若要建立的評估報告，請參閱[評估存取資料庫物件的轉換](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)。<br /><br />如果此問題，您必須確定主索引鍵沒有重複的 null 值。 或者，您必須移除主索引鍵或包含多個 null 值的唯一索引。|  
|存取資料表包含日期值超出的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]範圍。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Datetime**接受 1 年 1 月 1753 至 12 月 31 的範圍中的日期類型。 只有 9999。 存取接受 1 年 1 月 100，到 12 月 31 的範圍中的日期到 9999。<br /><br />SSMA 會加上旗標評估報告這個的問題。 若要建立的評估報告，請參閱[評估存取資料庫物件的轉換](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)。<br /><br />您可以設定如何 SSMA 解決日期出之[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]範圍。 如需詳細資訊，請參閱[（移轉） 的專案設定](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)。|  
|索引長度，以存取超過 900 個位元組。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]索引具有索引鍵資料行的總大小 900 個位元組限制。 如果您存取資料表使用較大的索引，SSMA 會顯示警告。<br /><br />如果您繼續資料移轉，移轉可能會失敗。|  
|存取物件名稱都[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]關鍵字，或包含特殊字元。|存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]具有不同組的保留的關鍵字和特殊字元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]將會接受物件的命名方式是使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]關鍵字，或包含特殊字元，如果您使用有括號或引號識別項，例如"select"或 [選取].p。 如需詳細資訊，請參閱 < 分隔識別碼 (Database Engine) > 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。<br /><br />**注意：**若要使用引號分隔識別碼，SET QUOTED_IDENTIFIER 必須是 ON。<br /><br />例如，`CREATE TABLE [schema](c1 [FOR])`是有效的陳述式，即使**結構描述**和**如**是保留的關鍵字。 此外，`CREATE TABLE [xxx*yyy](c1 x&y)`是有效的陳述式，即使資料表和資料行名稱包含特殊字元 **\&#42;**和 **&amp;** 。<br /><br />參考這些物件的所有查詢也必須都使用方括號或引號的名稱。 例如，查詢`SELECT * FROM schema`將會失敗。 正確的查詢是： `SELECT * FROM [schema]`。<br /><br />當您轉換來存取資料庫物件時，[輸出] 窗格會列出使用的關鍵字或特殊字元的任何存取資料表。 您可以修改資料表中存取，然後移除並將資料庫加入一次。或者，您可以修改，讓查詢使用方括號或引號來分隔識別碼參考這些物件的查詢。 如果您不要修改您的查詢，存取應用程式可能會傳回錯誤，或發生其他問題。|  
|欄位大小寫不同主索引鍵/外部索引鍵關聯性。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不支援連結具有不同的資料類型或大小與外部索引鍵條件約束的資料行的 Jet 功能。<br /><br />當您轉換來存取資料庫物件時，[輸出] 視窗會列出任何主索引鍵/外部索引鍵條件約束不會轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以變更資料類型和存取資料行的大小，使它們相符，然後移除並重新加入 Access 資料庫。 或者，您可以移轉資料，雖然這些條件約束將不會建立在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。|  
|存取關聯性中參考的資料表沒有主索引鍵也沒有唯一的索引。|存取會接受其中參考的資料表沒有主索引鍵或唯一索引鍵的資料表之間的關聯性。 不過，這不支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br />當您轉換來存取資料庫物件時，[輸出] 視窗會列出任何關聯性，但沒有主索引鍵或唯一索引的資料表。 您可以變更要加入主索引鍵或唯一索引，然後移除並重新加入 Access 資料庫的資料表。 或者，您可以移轉資料，雖然資料表之間的關聯性將會中斷。|  
|存取資料表有超連結資料行。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不支援**超連結**資料行。 相反地，資料行被視為存取備忘資料行。 根據預設，將這些資料行轉換成**nvarchar （max)**中的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以自訂對應。 如需詳細資訊，請參閱[對應來源和目標資料型別](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。|  
|預設值或驗證的規則運算式包含存取函式不能轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。|存取系統函式或未對應至使用者定義函數，則可能會包含存取預設運算式或驗證規則[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 不會對應到的函式的使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 會防止載入預設運算式或驗證規則加入至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。|  
  
## <a name="see-also"></a>請參閱  
[準備移轉的 Access 資料庫](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
