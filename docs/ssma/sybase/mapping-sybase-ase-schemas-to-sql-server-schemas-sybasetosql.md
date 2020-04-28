---
title: 將 Sybase ASE 架構對應至 SQL Server 架構（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5c39e81f8faffed606e6ca94315c47d383174c91
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028875"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>將 Sybase ASE 結構描述對應到 SQL Server 結構描述 (SybaseToSQL)
在 Sybase 調適型伺服器 Enterprise （ASE）中，每個資料庫都有一或多個架構。 根據預設，SSMA 會將資料庫和架構中的所有物件遷移至或 SQL Azure 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相同資料庫和架構。 不過，您可以自訂 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫和架構之間的對應。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 架構  
ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 都使用兩個部分標記法當做*資料庫*，來指定資料庫和其架構。 例如，在 ASE**示範**資料庫中，可能會有**dbo**架構。 該資料庫和架構配對會指定為**demo. dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 具有相同的資料庫和架構，則該配對也會指定為**demo. dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
在 SSMA 中，您可以將 ASE 架構對應至任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用或 SQL Azure 架構。  
  
**若要修改資料庫和架構**  
  
1.  在 [Sybase Metadata Explorer] 中，選取 [**資料庫**]。  
  
    當您選取個別資料庫、[**架構**] 資料夾或個別的架構時，也可以使用 [**架構對應**] 索引標籤。 [**架構對應**] 索引標籤中的清單是針對選取的物件自訂的。  
  
2.  在右窗格中，按一下 [**架構對應**] 索引標籤。  
  
    您會看到所有 ASE 資料庫的清單及其架構，後面接著目標值。 此目標是以或 SQL Azure 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的兩個部分標記法（*schema*）表示，而您的物件和資料將會在其中進行遷移。  
  
3.  選取包含您要變更之對應的資料列，然後按一下 [**修改**]。  
  
4.  在 [**選擇目標架構**] 對話方塊中，您可以流覽可用的目標資料庫和架構，或是在兩個部分標記法（Schema）的文字方塊中輸入資料庫和架構名稱，然後按一下 **[確定]**。  
  
5.  [**架構對應**] 索引標籤上的目標變更。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 根據預設，源資料庫會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不存在，則系統會提示您輸入「**資料庫和/或架構不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫下的非現有架構，這會在同步處理期間建立。  
  
-   對應至 SQL Azure  
  
您可以將源資料庫對應至已連線的目標 SQL Azure 資料庫或連接的目標 SQL Azure 資料庫中的任何架構。 如果您將來源架構對應至 [已連接的目標資料庫] 底下的任何非現有架構，則系統會提示您輸入「**架構不存在於目標中繼資料中」的訊息。它會在同步處理期間建立。您要繼續嗎？按一下 [是]。**  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原為預設資料庫和架構  
如果您自訂 ASE 架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 架構之間的對應，您可以將對應還原回預設值。  
  
**還原為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [**重設為預設值**]，以還原為預設資料庫和架構。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析 Sybase ASE 物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件的轉換，您可以[建立轉換報告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)。 否則，您可以[將 ASE 資料庫物件定義轉換](converting-sybase-ase-database-objects-sybasetosql.md)成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
