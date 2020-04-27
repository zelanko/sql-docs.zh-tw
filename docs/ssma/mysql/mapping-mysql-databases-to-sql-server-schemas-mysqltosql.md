---
title: 將 MySQL 資料庫對應至 SQL Server 架構（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 215833c96fae02ae7877e00173fb5a920a47ee0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908982"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>將 MySQL 資料庫對應到 SQL Server 結構描述 (MySQLToSQL)
根據預設，適用于 MySQL 的 SSMA 會將 MySQL 架構中的所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件遷移至名為的或 SQL Azure 資料庫，做為架構。 不過，您可以自訂 MySQL 架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫之間的對應。  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL 和 SQL Server 或 SQL Azure 架構  
架構的 MySQL 概念會對應到資料庫的 SQL Server 概念及其其中一個架構。 SSMA 指的是資料庫和架構的 SQL Server 組合，做為架構。  
  
架構的 MySQL 概念會對應到資料庫的 SQL Server 概念及其其中一個架構。 例如，MySQL 可能會有一個名為**HR**的架構。 SQL Server 的實例可能會有一個名為**HR**的資料庫，而該資料庫內則為架構。 其中一個架構是**dbo** （或資料庫擁有者）架構。 根據預設，MySQL 架構**hr**會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構**hr. dbo**。 SSMA 是指將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構結合為架構。  
  
您可以修改 MySQL 與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure 架構之間的對應。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
在 SSMA 中，您可以將 MySQL 架構對應到任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用或 SQL Azure 架構。  
  
**若要修改資料庫和架構**  
  
1.  在 MySQL 中繼資料 Explorer 中，選取 [**架構**]。  
  
    當您選取個別的架構時，也可以使用 [**架構對應**] 索引標籤。 [**架構對應**] 索引標籤中的清單是針對選取的物件自訂的。  
  
2.  在右窗格中，按一下 [**架構對應**] 索引標籤。  
  
    您會看到所有 MySQL 架構的清單，後面接著目標值。 此目標是以或 SQL Azure 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的兩個部分標記法（*schema*）表示，而您的物件和資料將會在其中進行遷移。  
  
3.  選取包含您要變更之對應的資料列，然後按一下 [**修改**]。  
  
    在 [**選擇目標架構**] 對話方塊中，您可以流覽可用的目標資料庫和架構，或是在兩個部分標記法（Schema）的文字方塊中輸入資料庫和架構名稱，然後按一下 **[確定]**。  
  
4.  [**架構對應**] 索引標籤上的目標變更。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 根據預設，源資料庫會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不存在，則系統會提示您輸入「**資料庫和/或架構不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫下的非現有架構，這會在同步處理期間建立。  
  
-   對應至 SQL Azure  
  
您可以將源資料庫對應到連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，或對應至連接的目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的任何架構。 如果您將來源架構對應至 [已連接的目標資料庫] 底下的任何非現有架構，則系統會提示您輸入「**架構不存在於目標中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？按一下 [是]。**  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原為預設資料庫和架構  
如果您自訂 MySQL 架構與 SQL Server 架構之間的對應，您可以將對應還原回預設值。  
  
**還原為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [**重設為預設值**]，以還原為預設資料庫和架構。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析將 MySQL 物件轉換成 SQL Server 或 SQL Azure 物件，您可以[建立轉換報告](assessing-mysql-databases-for-conversion-mysqltosql.md)，否則您可以[將 mysql 資料庫物件定義轉換](converting-mysql-databases-mysqltosql.md)成 SQL Server 或 sql azure 架構  
  
## <a name="see-also"></a>另請參閱  
[專案設定 &#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[連接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
