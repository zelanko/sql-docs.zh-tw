---
title: 將 DB2 結構描述對應至 SQL Server 結構描述 (DB2ToSQL) |Microsoft Docs
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
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b745050556a0fa21d57daaf09bc21f7d4bbc93cf
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "40392038"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>將 DB2 結構描述對應至 SQL Server 結構描述 (DB2ToSQL)
DB2，在每個資料庫會有一或多個結構描述。 根據預設，SSMA 會移轉 DB2 結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名為結構描述的資料庫。 不過，您可以自訂 DB2 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 和 SQL Server 結構描述  
DB2 資料庫包含結構描述。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包含多個資料庫，每一個都可以有多個結構描述。  
  
DB2 結構描述的概念對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和其結構描述的其中一個的概念。 例如，DB2 可能名為結構描述**HR**。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能會有一個名為資料庫**HR**，而該資料庫中則為結構描述。 是一個結構描述**dbo** （或資料庫擁有者） 結構描述。 根據預設，DB2 結構描述**HR**將會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述的組合，當做結構描述。  
  
您可以修改 DB2 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改結構描述與目標資料庫  
SSMA 中，您可以將 DB2 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 [DB2 中繼資料總管] 中，選取**結構描述**。  
  
    **結構描述對應**索引標籤也會提供當您選取個別的資料庫，**結構描述**資料夾或個別的結構描述。 中的清單**結構描述對應**自訂所選物件的索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到所有的 DB2 結構描述，後面接著目標值的清單。 此目標，則表示兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
    在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫和結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**.  
  
4.  變更目標**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標的資料庫。 根據預設值對應的來源資料庫至目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與您已連線使用 SSMA 的資料庫。 要對應的目標資料庫使用時間是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則您將會出現一個訊息 **"的資料庫和/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料。它會在同步處理期間被建立。您要繼續嗎？"** 按一下 [是]。 同樣地，您可以將結構描述對應至不存在的結構描述目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在同步處理期間建立的資料庫。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂的 DB2 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述中，您可以還原回預設值的對應。  
  
**若要還原成預設的資料庫和結構描述**  
  
1.  在 [結構描述對應] 索引標籤中，選取任何資料列然後按一下**重設為預設**還原成預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 DB2 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件，您可以[（SSMA 常見） 的資料移轉報告](http://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)。  
  
## <a name="see-also"></a>另請參閱  
[連接到 SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[移轉的 DB2 資料庫到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
