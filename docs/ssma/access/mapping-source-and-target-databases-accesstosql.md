---
title: 對應來源和目標資料庫（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 192db2e6c074305ca258d76652351175c8a82751
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907151"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>對應來源和目標資料庫（AccessToSQL）
當您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 時，您需要指定要進行遷移的目標資料庫。 如果您有多個 Access 資料庫，您可以將它們[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]對應至多個資料庫（或架構），或對應到已連線之 SQL Azure 資料庫下的多個架構。  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 或 SQL Azure 資料庫架構  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫會使用架構的概念，將資料庫內的物件分隔成邏輯群組。 例如，程式庫資料庫可以使用名為「**書籍**」、「**音訊**」和「**影片**」的三個架構來分隔書籍、音訊和影片物件。 根據預設，access 資料庫會對應到**master**資料庫，以及**** 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 dbo 架構和 SQL Azure 中的連接資料庫和**dbo**架構。  
  
除非您自訂每個 Access 資料庫與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構之間的對應，否則 SSMA 會將與 Access 資料庫相關聯的所有架構和資料移轉到預設的資料庫對應。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
SSMA 可讓您將每個 Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫對應到或 SQL Azure 資料庫和架構。 下列程式描述如何自訂每個資料庫的對應。  
  
**修改目標資料庫和架構**  
  
1.  在 [存取中繼資料瀏覽器] 窗格中，選取 [**存取-中繼資料**]。  
  
    當您選取 [**資料庫**] 節點或任何資料庫節點時，也可以使用架構對應。 已針對選取的物件自訂架構對應清單。  
  
2.  在右窗格中，按一下 [**架構對應**] 索引標籤。  
  
    您會看到一個資料表，其中包含 access 資料庫名稱及其對應的 ssNoVersion 或 Sql Azure 架構。 目標架構會以兩個部分的標記法（database. schema）來表示。  
  
3.  選取包含您要自訂之對應的資料列，然後按一下 [**修改**]。  
  
4.  在 [**選擇目標架構**] 對話方塊中，您可以流覽可用的目標資料庫和架構，或是在兩個部分標記法（Schema）的文字方塊中輸入資料庫和架構名稱，然後按一下 **[確定]**。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 根據預設，源資料庫會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫不存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，則系統會提示您輸入「**資料庫和/或架構不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫下的非現有架構，這會在同步處理期間建立。  
  
-   對應至 SQL Azure  
  
您可以將源資料庫對應到連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，或對應至連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的任何架構。 如果您將來源架構對應至 [已連接的目標資料庫] 底下的任何非現有架構，則系統會提示您輸入「**架構不存在於目標中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？按一下 [是]。**  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>還原成您的初始資料庫和架構  
如果您自訂 Access 資料庫和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 資料庫和架構之間的對應，您可以將對應還原回連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 時所指定的資料庫。  
  
**若要重設為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [**重設為預設值**]，以還原為預設資料庫和架構。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[轉換資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
