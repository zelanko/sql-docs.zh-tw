---
title: 將 Oracle 結構描述對應至 SQL Server 結構描述 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 5e231fd84b85a44392527e7f082b55da1c7826ac
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393809"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>將 Oracle 結構描述對應到 SQL Server 結構描述 (OracleToSQL)
在 Oracle 中，每個資料庫會有一或多個結構描述。 根據預設，SSMA 會移轉 Oracle 結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名為結構描述的資料庫。 不過，您可以自訂 Oracle 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle 和 SQL Server 結構描述  
Oracle 資料庫包含結構描述。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包含多個資料庫，每一個都可以有多個結構描述。  
  
Oracle 結構描述的概念對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和其結構描述的其中一個的概念。 例如，Oracle 可能名為結構描述**HR**。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能會有一個名為資料庫**HR**，而該資料庫中則為結構描述。 是一個結構描述**dbo** （或資料庫擁有者） 結構描述。 根據預設，Oracle 結構描述**HR**將會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述**HR.dbo**。 SSMA 是指[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫和結構描述的組合，當做結構描述。  
  
您可以修改 Oracle 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改結構描述與目標資料庫  
SSMA 中，您可以將 Oracle 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  在 Oracle 中繼資料總管 中，選取**結構描述**。  
  
    **結構描述對應**索引標籤也會提供當您選取個別的資料庫，**結構描述**資料夾或個別的結構描述。 中的清單**結構描述對應**自訂所選物件的索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到所有的 Oracle 結構描述，後面接著目標值的清單。 此目標，則表示兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中將會移轉您的物件和資料。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
    在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫和結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**.  
  
4.  變更目標**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標的資料庫。 根據預設值對應的來源資料庫至目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與您已連線使用 SSMA 的資料庫。 要對應的目標資料庫使用時間是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則您將會出現一個訊息 **"的資料庫和/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料。它會在同步處理期間被建立。您要繼續嗎？"** 按一下 [是]。 同樣地，您可以將結構描述對應至不存在的結構描述目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在同步處理期間建立的資料庫。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂的 Oracle 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述中，您可以還原回預設值的對應。  
  
**若要還原成預設的資料庫和結構描述**  
  
1.  在 [結構描述對應] 索引標籤中，選取任何資料列然後按一下**重設為預設**還原成預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>後續步驟  
如果您想要分析的 Oracle 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件，您可以[建立轉換報告](assessing-oracle-schemas-for-conversion-oracletosql.md)。 否則您可以[轉換的 Oracle 資料庫物件定義](converting-oracle-schemas-oracletosql.md)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件定義。  
  
## <a name="see-also"></a>另請參閱  
[連接到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
