---
title: 對應來源和目標資料庫 (AccessToSQL) |Microsoft 文件
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
manager: craigg
ms.openlocfilehash: d2be7854240a52edd8f3308ea92e3ea7eb25924f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299194"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>對應來源和目標資料庫 (AccessToSQL)
當您連線至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您必須指定目標資料庫，以便進行移轉。 如果您有多個 Access 資料庫中您就可以將它們對應至多個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫 （或結構描述） 或在連線的 SQL Azure 資料庫的多個結構描述。  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server 或 SQL Azure 的資料庫結構描述  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫會使用結構描述的概念來分隔成邏輯群組的資料庫中的物件。 例如，程式庫資料庫無法使用三個結構描述，名為**書籍**，**音訊**，和**視訊**來彼此分隔活頁簿時，音訊及視訊的物件。 根據預設，access 資料庫對應至**主要**資料庫和**dbo**結構描述中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和連接的資料庫和**dbo** SQL Azure 中的結構描述。  
  
除非您來自訂每一個 Access 資料庫之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述，SSMA 會移轉所有的結構描述和對應的預設資料庫的 access 資料庫與相關聯的資料。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改結構描述與目標資料庫  
SSMA 可讓您對應至每個 Access 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫和結構描述。 下列程序說明如何自訂每個資料庫的對應。  
  
**若要修改結構描述與目標資料庫**  
  
1.  在 存取中繼資料檔案總管 窗格中，選取 **存取中繼資料**。  
  
    當您選取時，還有可用的結構描述對應**資料庫**節點或任何資料庫節點。 所選物件的自訂結構描述的對應清單。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到表格，包含存取資料庫的名稱及其對應的 ssNoVersion 或 Sql Azure 結構描述。 目標結構描述是在兩個組件標記法 (database.schema) 表示。  
  
3.  選取包含您想要自訂，然後按一下的對應的資料列**修改**。  
  
4.  在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫和結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**.  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標的資料庫。 根據預設值對應的來源資料庫至目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與您已連線使用 SSMA 的資料庫。 如果要對應之目標資料庫不存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則您將會出現一個訊息 **"的資料庫和/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料。它會在同步處理期間被建立。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將結構描述對應至不存在的結構描述目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在同步處理期間建立的資料庫。  
  
-   對應至 SQL Azure  
  
您可以將來源資料庫對應至連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫或連接的目標中的任何結構描述至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 如果您將來源結構描述對應至連接的目標資料庫底下的任何非現有結構描述，則您將會出現一個訊息 **」 結構描述不存在於目標中繼資料。它會在同步處理期間被建立。您要繼續嗎？"** 按一下 [是]。  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>還原到您的初始資料庫和結構描述  
如果您自訂 Access 資料庫之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫和結構描述，您便可還原回您指定當您連接到資料庫的對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
**若要重設回預設資料庫及結構描述**  
  
1.  在 [結構描述對應] 索引標籤中，選取任何資料列然後按一下**重設為預設**還原成預設的資料庫和結構描述。  
  
## <a name="next-step"></a>下一個步驟  
遷移程序的下一個步驟是[轉換資料庫物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
