---
title: 將 Oracle 架構對應至 SQL Server 架構（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e375c07ceddc995b599930c14f00710af040d6c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68262907"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>將 Oracle 結構描述對應到 SQL Server 結構描述 (OracleToSQL)
在 Oracle 中，每個資料庫都有一或多個架構。 根據預設，SSMA 會將 Oracle 架構中的所有物件遷移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至架構名稱為的資料庫。 不過，您可以自訂 Oracle 架構與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫之間的對應。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 和 SQL Server 架構  
Oracle 資料庫包含架構。 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例包含多個資料庫，其中每一個都可以有多個架構。  
  
架構的 Oracle 概念會對應到資料庫的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]概念，以及它的其中一個架構。 例如，Oracle 可能會有一個名為**HR**的架構。 的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能具有名為**HR**的資料庫，而且在該資料庫內為架構。 其中一個架構是**dbo** （或資料庫擁有者）架構。 根據預設，Oracle 架構**hr**會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構**hr. dbo**。 SSMA 是指將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和架構結合為架構。  
  
您可以修改 Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構之間的對應。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
在 SSMA 中，您可以將 Oracle 架構對應到任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用的架構。  
  
**若要修改資料庫和架構**  
  
1.  在 [Oracle 中繼資料 Explorer] 中，選取 [**架構**]。  
  
    當您選取個別資料庫、[**架構**] 資料夾或個別的架構時，也可以使用 [**架構對應**] 索引標籤。 [**架構對應**] 索引標籤中的清單是針對選取的物件自訂的。  
  
2.  在右窗格中，按一下 [**架構對應**] 索引標籤。  
  
    您會看到所有 Oracle 架構的清單，後面接著目標值。 此目標會以兩個部分標記法（*database. schema*）表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，其中您的物件和資料將會遷移到其中。  
  
3.  選取包含您要變更之對應的資料列，然後按一下 [**修改**]。  
  
    在 [**選擇目標架構**] 對話方塊中，您可以流覽可用的目標資料庫和架構，或是在兩個部分標記法（Schema）的文字方塊中輸入資料庫和架構名稱，然後按一下 **[確定]**。  
  
4.  [**架構對應**] 索引標籤上的目標變更。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 根據預設，源資料庫會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不存在，則系統會提示您輸入「**資料庫和/或架構不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫下的非現有架構，這會在同步處理期間建立。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原為預設資料庫和架構  
如果您自訂 Oracle 架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構之間的對應，您可以將對應還原回預設值。  
  
**還原為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [**重設為預設值**]，以還原為預設資料庫和架構。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析 Oracle 物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件的情況，您可以[建立轉換報表](assessing-oracle-schemas-for-conversion-oracletosql.md)。 否則，您可以[將 Oracle 資料庫物件定義轉換](converting-oracle-schemas-oracletosql.md)成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件定義。  
  
## <a name="see-also"></a>另請參閱  
[連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
