---
description: 將 Sybase ASE 結構描述對應到 SQL Server 結構描述 (SybaseToSQL)
title: 將 Sybase ASE 架構對應至 SQL Server 架構 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: db0c65c8def8c2a755fe6ca9a224c936e9085f8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320194"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>將 Sybase ASE 結構描述對應到 SQL Server 結構描述 (SybaseToSQL)
在 Sybase 自調適型 Server Enterprise (ASE) 中，每個資料庫都有一或多個架構。 根據預設，SSMA 會將資料庫和架構內的所有物件遷移至或 SQL Azure 中的相同資料庫和架構 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 不過，您可以自訂 ASE 和或 Azure SQL Database 之間的對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 架構  
ASE 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 都使用兩個部分標記法作為 *資料庫*，來指定資料庫及其架構。 例如，在 ASE **示範** 資料庫中，可能會有 **dbo** 架構。 該資料庫和架構組會指定為 **demo. dbo**。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 具有相同的資料庫和架構，則該配對也會指定為 **demo. dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和架構  
在 SSMA 中，您可以將 ASE 架構對應至任何可用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 架構。  
  
**若要修改資料庫和架構**  
  
1.  在 [Sybase 中繼資料瀏覽器] 中，選取 [ **資料庫**]。  
  
    當您選取個別的資料庫、**架構**資料夾或個別的架構時，也可以使用 [**架構對應**] 索引標籤。 [ **架構對應** ] 索引標籤中的清單是針對選取的物件自訂的。  
  
2.  在右窗格中，按一下 [ **架構對應** ] 索引標籤。  
  
    您將會看到所有 ASE 資料庫的清單及其架構，後面接著一個目標值。 這個目標以兩個部分標記法表示 (*資料庫。架構*) 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 中，您的物件和資料將會遷移到其中。  
  
3.  選取包含您要變更之對應的資料列，然後按一下 [ **修改**]。  
  
4.  在 [ **選擇目標架構** ] 對話方塊中，您可以流覽可用的目標資料庫和架構，或在兩個部分標記法 () 資料庫中，于文字方塊中輸入資料庫和架構名稱，然後按一下 **[確定]**。  
  
5.  [ **架構對應** ] 索引標籤上的目標變更。  
  
**對應模式**  
  
-   對應至 SQL Server  
  
您可以將源資料庫對應到任何目標資料庫。 依預設，源資料庫會對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您已使用 SSMA 連接的目標資料庫。 如果要對應的目標資料庫不 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存在，則系統會提示您輸入訊息 **：「資料庫和/或架構不存在於目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料中。它會在同步處理期間建立。您要繼續嗎？** 」 按一下 [是]。 同樣地，您可以將架構對應至目標資料庫下的非現有架構 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （將在同步處理期間建立）。  
  
-   對應至 SQL Azure  
  
您可以將源資料庫對應到連接的目標 Azure SQL Database 或連接的目標 Azure SQL Database 中的任何架構。 如果您將來源架構對應到連接的目標資料庫下的任何非現有架構，系統將會提示您輸入訊息 **：「架構不存在於目標中繼資料中。它會在同步處理期間建立。您要繼續嗎？按一下 [是]。**  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原為預設資料庫和架構  
如果您自訂 ASE 架構與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 架構之間的對應，您可以將對應還原回預設值。  
  
**還原為預設資料庫和架構**  
  
1.  在 [架構對應] 索引標籤下，選取任何資料列，然後按一下 [ **重設為預設值** ]，還原成預設的資料庫和架構。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析 Sybase ASE 物件至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 物件的轉換，您可以 [建立轉換報表](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)。 否則，您可以 [將 ASE 資料庫物件定義轉換](converting-sybase-ase-database-objects-sybasetosql.md) 成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 物件定義。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
