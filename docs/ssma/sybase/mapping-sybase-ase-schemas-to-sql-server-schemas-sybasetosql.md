---
title: 將 Sybase ASE 結構描述對應至 SQL Server 結構描述 (SybaseToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2a27b2e7c915a1ac13050d0ed188002cd42746c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62705933"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>將 Sybase ASE 結構描述對應到 SQL Server 結構描述 (SybaseToSQL)
在 Sybase Adaptive Server Enterprise (ASE)，每個資料庫有一或多個結構描述。 根據預設，SSMA，請移轉到相同的資料庫和結構描述中的資料庫和結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 不過，您可以自訂 ASE 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫和結構描述。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 結構描述  
ASE 並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫和其結構描述使用兩個部分表示法指定為*database.schema*。 例如，在 ASE **demo**資料庫，可能會有**dbo**結構描述。 資料庫和結構描述的組合會指定為**demo.dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 有相同的資料庫和結構描述，配對也指定成**demo.dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改結構描述與目標資料庫  
SSMA 中，您可以將 ASE 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 Sybase 中繼資料總管 中，選取**資料庫**。  
  
    **結構描述對應**索引標籤也會提供當您選取個別的資料庫，**結構描述**資料夾或個別的結構描述。 中的清單**結構描述對應**自訂所選物件的索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到一份所有 ASE 資料庫結構描述中，後面接著目標值。 此目標，則表示兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
4.  在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫和結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**.  
  
5.  變更目標**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標的資料庫。 根據預設值對應的來源資料庫至目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與您已連線使用 SSMA 的資料庫。 要對應的目標資料庫使用時間是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則您將會出現一個訊息 **"的資料庫和/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料。它會在同步處理期間被建立。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將結構描述對應至不存在的結構描述目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在同步處理期間建立的資料庫。  
  
-   對應至 SQL Azure  
  
您可以在連接的目標 SQL Azure 資料庫或連接的目標 SQL Azure 資料庫中的任何結構描述對應來源資料庫。 如果您將來源結構描述對應至連接的目標資料庫底下的任何非現有結構描述，則您將會出現一個訊息 **」 結構描述不存在於目標中繼資料。它會在同步處理期間被建立。您要繼續嗎？"** 按一下 [是]。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂的 ASE 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 結構描述中，您可以還原回預設值的對應。  
  
**若要還原成預設的資料庫和結構描述**  
  
1.  在 [結構描述對應] 索引標籤中，選取任何資料列然後按一下**重設為預設**還原成預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 Sybase ASE 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件，您可以[建立轉換報告](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)。 否則您可以[轉換 ASE 資料庫物件定義](converting-sybase-ase-database-objects-sybasetosql.md)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件定義。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
