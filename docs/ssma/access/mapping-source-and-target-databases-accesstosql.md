---
title: 對應來源和目標資料庫 (AccessToSQL) |Microsoft Docs
description: 瞭解如何指定目標資料庫來進行 Access 資料庫移轉，以 SQL Server 或 Azure SQL Database，包括多個資料庫到多個資料庫。
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9e07c42e272728943f30198c8800c86aaa9443e3
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938113"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>對應來源和目標資料庫 (AccessToSQL) 
當您連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 時，您需要指定要進行遷移的目標資料庫。 如果您有多個 Access 資料庫，您可以將它們對應至多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫 (或架構) 或連接 Azure SQL Database 下的多個架構。  
  
## <a name="sql-server-or-azure-sql-database-schemas"></a>SQL Server 或 Azure SQL Database 架構  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫會使用架構的概念，將資料庫內的物件分隔成邏輯群組。 例如，程式庫資料庫可以使用名為「**書籍**」、「**音訊**」和「**影片**」的三個架構來分隔書籍、音訊和影片物件。 根據預設，access 資料庫會對應到**master**資料庫，以及中的**DBO**架構和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 中的連接資料庫和**dbo**架構。  
  
除非您自訂每個 Access 資料庫與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫和架構之間的對應，否則 SSMA 會將與 Access 資料庫相關聯的所有架構和資料移轉到預設的資料庫對應。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
SSMA 可讓您將每個 Access 資料庫對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 下列程式描述如何自訂每個資料庫的對應。  
  
**修改目標資料庫和架構**  
  
1.  在 [存取中繼資料瀏覽器] 窗格中，選取 [**存取-中繼資料**]。  
  
    當您選取 [**資料庫**] 節點或任何資料庫節點時，也可以使用架構對應。 已針對選取的物件自訂架構對應清單。  
  
2.  在右窗格中，按一下 [**架構對應**] 索引標籤。  
  
    您會看到一個資料表，其中包含 access 資料庫名稱及其對應的 ssNoVersion 或 Sql Azure 架構。 目標架構會以兩個部分的標記法表示 (資料庫。架構) 。  
  
3.  選取包含您要自訂之對應的資料列，然後按一下 [**修改**]。  
  
4.  在 [**選擇目標架構**] 對話方塊中，您可以流覽可用的目標資料庫和架構，或是在兩個部分的標記法中輸入資料庫和架構名稱 (database. 架構) 然後按一下 **[確定]**。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 根據預設，源資料庫會對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫不存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，則系統會提示您輸入「**資料庫和/或架構不存在於目標中繼資料中」的訊息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應到目標資料庫下的非現有架構， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這會在同步處理期間建立。  
  
-   對應至 SQL Azure  
  
您可以將源資料庫對應到連接的目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，或對應至連接的目標資料庫中的任何架構 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您將來源架構對應至 [已連接的目標資料庫] 底下的任何非現有架構，則系統會提示您輸入「**架構不存在於目標中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？按一下 [是]。**  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>還原成您的初始資料庫和架構  
如果您自訂 Access 資料庫與或 Azure SQL Database 之間的對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以將對應還原回連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 時所指定的資料庫。  
  
**若要重設為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [**重設為預設值**]，以還原為預設資料庫和架構。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[轉換資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
