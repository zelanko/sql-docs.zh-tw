---
title: Sybase ASE 結構描述對應至 SQL Server 結構描述 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e0b8dad8d5742782ed3b3828806c5122092b37b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Sybase ASE 結構描述對應至 SQL Server 結構描述 (SybaseToSQL)
在 Sybase Adaptive Server Enterprise (ASE)，每個資料庫有一或多個結構描述。 根據預設，SSMA，請移轉到相同的資料庫和結構描述中的資料庫和結構描述中的所有物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 不過，您可以自訂 ASE 之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫和結構描述。  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE 和 SQL Server 或 SQL Azure 的結構描述  
ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫和其結構描述使用兩個部分表示法指定為*database.schema*。 例如，在 ase 中**示範**資料庫，可能會有**dbo**結構描述。 一組資料庫和結構描述會指定為**demo.dbo**。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 有相同的資料庫和結構描述，配對也指定成**demo.dbo**。  
  
## <a name="modifying-the-target-database-and-schema"></a>修改目標資料庫和結構描述  
SSMA，在您可以將 ASE 結構描述對應到任何可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 結構描述。  
  
**若要修改的資料庫和結構描述**  
  
1.  Sybase 中繼資料總管，在選取**資料庫**。  
  
    **結構描述對應** 索引標籤也會提供當您選取個別資料庫，**結構描述**資料夾或個別結構描述。 中的清單**結構描述對應**所選物件的自訂索引標籤。  
  
2.  在右窗格中，按一下 [**結構描述對應**] 索引標籤。  
  
    您會看到一份所有 ASE 資料庫結構描述中，後面接著目標值。 此目標，則表示在兩個組件標記法 (*database.schema*) 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您的物件和資料將會移轉。  
  
3.  選取包含您想要變更，然後再按一下對應的資料列**修改**。  
  
4.  在**選擇目標結構描述**對話方塊中，您可能瀏覽可用的目標資料庫和結構描述或型別資料庫結構描述] 文字方塊中的兩個組件標記法 (database.schema) 中的名稱，然後按一下 [**確定**。  
  
5.  目標上的變更**結構描述對應** 索引標籤。  
  
**對應的模式**  
  
-   對應至 SQL Server  
  
您可以將來源資料庫對應到任何目標資料庫。 依預設，來源資料庫都會對應到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]與您已經連接使用 SSMA 的資料庫。 正在對應之目標資料庫是否不存在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，則會以訊息提示您**」 資料庫及/或結構描述不存在於目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料。它會建立同步處理期間。您要繼續嗎？ 」** 按一下 [是]。 同樣地，您可以將對應結構描述不存在目標結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同步處理期間所建立的資料庫。  
  
-   對應至 SQL Azure  
  
若要連接的目標 SQL Azure 資料庫或連接的目標 SQL Azure 資料庫中任何結構描述，您可以對應來源資料庫。 如果您將來源結構描述對應至連接的目標資料庫底下的任何非現有結構描述，則系統將提示您使用訊息**」 結構描述不存在於目標中繼資料。它會建立同步處理期間。您要繼續嗎？"**按一下 [是]。  
  
## <a name="reverting-to-the-default-database-and-schema"></a>還原成預設的資料庫和結構描述  
如果您自訂 ASE 結構描述之間的對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的結構描述，您可以還原回預設值的對應。  
  
**若要還原為預設的資料庫和結構描述**  
  
1.  結構描述對應索引標籤下選取任何資料列，然後按一下**重設為預設**還原為預設的資料庫和結構描述。  
  
## <a name="next-steps"></a>Next Steps  
如果您想要分析的 Sybase ASE 物件到轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，您可以[建立轉換報告](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)。 您可以在否則[轉換 ASE 資料庫物件定義](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3)到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件定義。  
  
## <a name="see-also"></a>請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
