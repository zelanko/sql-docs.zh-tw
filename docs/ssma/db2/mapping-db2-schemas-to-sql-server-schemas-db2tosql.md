---
title: "DB2 結構描述對應至 SQL Server 結構描述 (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e422c99f45b5da02214aee96bb0520dc8c851e74
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>DB2 結構描述對應至 SQL Server 結構描述 (DB2ToSQL)
DB2，在每個資料庫會有一或多個結構描述。 根據預設，SSMA 會移轉 DB2 結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]名為結構描述的資料庫。 不過，您可以自訂 DB2 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 與 SQL Server 結構描述  
DB2 資料庫包含結構描述。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]包含多個資料庫，其中每一個都可以有多個結構描述。  
  
DB2 的概念結構描述對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫且其中一個其結構描述的概念。 例如，DB2 可能名為結構描述**HR**。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可能有一個名為資料庫**HR**，而且該資料庫內結構描述。 一個結構描述是**dbo** （或資料庫擁有者） 結構描述。 根據預設，DB2 結構描述**HR**將會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]為結構描述資料庫和結構描述的組合。  
  
您可以修改 DB2 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和結構描述  
SSMA，在您可以將 DB2 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 DB2 中繼資料總管，選取**結構描述**。  
  
    **結構描述對應** 索引標籤也會提供當您選取個別資料庫，**結構描述**資料夾或個別結構描述。 中的清單**結構描述對應**所選物件的自訂索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到所有的 DB2 結構描述，後面接著目標值的清單。 此目標，則表示在兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
    在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**。  
  
4.  目標上的變更**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標資料庫。 依預設，來源資料庫都會對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]與您已經連接使用 SSMA 的資料庫。 正在對應之目標資料庫是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，則會以訊息提示您**」 資料庫及/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。它會建立同步處理期間。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將對應結構描述不存在目標結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同步處理期間所建立的資料庫。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂的 DB2 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述中，您可以還原回預設值的對應。  
  
**若要還原為預設的資料庫和結構描述**  
  
1.  結構描述對應索引標籤下選取任何資料列，然後按一下**重設為預設**還原為預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 DB2 將物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，您可以[（SSMA 通用） 的資料移轉報告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)。  
  
## <a name="see-also"></a>請參閱＜  
[連接到 SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[DB2 資料庫移轉至 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
