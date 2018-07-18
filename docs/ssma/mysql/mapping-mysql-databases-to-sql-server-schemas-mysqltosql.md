---
title: 將 MySQL 資料庫對應至 SQL Server 結構描述 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 87720daab47ce4d21e7232b08b81e97b8171f43d
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980530"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>將 MySQL 資料庫對應至 SQL Server 結構描述 (MySQLToSQL)
根據預設，SSMA for MySQL 移轉 MySQL 結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或名為結構描述的 SQL Azure 資料庫。 不過，您可以自訂 MySQL 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL 和 SQL Server 或 SQL Azure 結構描述  
MySQL 概念結構描述會對應至 SQL Server 的概念，資料庫以及其結構描述的其中一個。 SSMA 是指 SQL Server 組合的資料庫和結構描述做為結構描述。  
  
MySQL 概念結構描述會對應至 SQL Server 的概念，資料庫以及其結構描述的其中一個。 例如，MySQL 可能名為結構描述**HR**。 SQL Server 的執行個體可能有一個名為資料庫**HR**，而該資料庫中則為結構描述。 是一個結構描述**dbo** （或資料庫擁有者） 結構描述。 根據預設，MySQL 結構描述**HR**將會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述的組合，當做結構描述。  
  
您可以修改 MySQL 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure 的結構描述。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改結構描述與目標資料庫  
SSMA 中，您可以將 MySQL 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 [MySQL 中繼資料總管] 中，選取**結構描述**。  
  
    **結構描述對應** 索引標籤也會提供當您選取個別結構描述。 中的清單**結構描述對應**自訂所選物件的索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到所有的 MySQL 結構描述，後面接著目標值的清單。 此目標，則表示兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
    在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫和結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**.  
  
4.  變更目標**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標的資料庫。 根據預設值對應的來源資料庫至目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]與您已連線使用 SSMA 的資料庫。 要對應的目標資料庫使用時間是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，則您將會出現一個訊息 **"的資料庫和/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。它會在同步處理期間被建立。您要繼續嗎？"** 按一下 [是]。 同樣地，您可以將結構描述對應至不存在的結構描述目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]會在同步處理期間建立的資料庫。  
  
-   對應至 SQL Azure  
  
您可以將來源資料庫對應至連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫或連接的目標中的任何結構描述至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 如果您將來源結構描述對應到在連線的目標資料庫的任何非現有結構描述，那麼您將會出現一個訊息 **"結構描述不存在於目標中繼資料。它會在同步處理期間被建立。您想要繼續嗎？"** 按一下 [是]。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂的 MySQL 結構描述和 SQL Server 結構描述之間的對應，您可以還原回預設值的對應。  
  
**若要還原成預設的資料庫和結構描述**  
  
1.  在 [結構描述對應] 索引標籤中，選取任何資料列然後按一下**重設為預設**還原成預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 MySQL 物件轉換成 SQL Server 或 SQL Azure 的物件，您可以[建立轉換報告](http://msdn.microsoft.com/2a56a003-3b0f-453a-963c-00c9e40933ec)否則您可以[轉換 MySQL 資料庫物件定義](http://msdn.microsoft.com/ac21850b-fb32-4704-9985-5759b7c688c7)成 SQL伺服器或 SQL Azure 的結構描述  
  
## <a name="see-also"></a>另請參閱  
[專案設定&#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[連線到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
