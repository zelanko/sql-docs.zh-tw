---
title: "Oracle 結構描述對應至 SQL Server 結構描述 (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ca4fbcf3a49ccaf289bab39e3dbd15493fe08bb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Oracle 結構描述對應至 SQL Server 結構描述 (OracleToSQL)
在 Oracle 中，每個資料庫有一或多個結構描述。 根據預設，SSMA 會移轉 Oracle 結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]名為結構描述的資料庫。 不過，您可以自訂 Oracle 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 和 SQL Server 結構描述  
Oracle 資料庫包含結構描述。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]包含多個資料庫，其中每一個都可以有多個結構描述。  
  
Oracle 的概念結構描述對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫且其中一個其結構描述的概念。 例如，Oracle 可能名為結構描述**HR**。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可能有一個名為資料庫**HR**，而且該資料庫內結構描述。 一個結構描述是**dbo** （或資料庫擁有者） 結構描述。 根據預設，Oracle 結構描述**HR**將會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫和結構描述**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]為結構描述資料庫和結構描述的組合。  
  
您可以修改 Oracle 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和結構描述  
SSMA，在您可以將 Oracle 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 Oracle 中繼資料總管，選取**結構描述**。  
  
    **結構描述對應** 索引標籤也會提供當您選取個別資料庫，**結構描述**資料夾或個別結構描述。 中的清單**結構描述對應**所選物件的自訂索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到所有的 Oracle 結構描述，後面接著目標值的清單。 此目標，則表示在兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
    在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**。  
  
4.  目標上的變更**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標資料庫。 依預設，來源資料庫都會對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]與您已經連接使用 SSMA 的資料庫。 正在對應之目標資料庫是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，則會以訊息提示您**」 資料庫及/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。它會建立同步處理期間。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將對應結構描述不存在目標結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同步處理期間所建立的資料庫。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂在 Oracle 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述中，您可以還原回預設值的對應。  
  
**若要還原為預設的資料庫和結構描述**  
  
1.  結構描述對應索引標籤下選取任何資料列，然後按一下**重設為預設**還原為預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 Oracle 物件到轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，您可以[建立轉換報告](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)。 您可以在否則[轉換 Oracle 資料庫物件定義](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件定義。  
  
## <a name="see-also"></a>另請參閱  
[連接到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[將 Oracle 資料庫移轉至 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

