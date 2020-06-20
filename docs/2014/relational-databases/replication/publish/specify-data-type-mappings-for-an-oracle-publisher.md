---
title: 指定 Oracle 發行者的資料類型對應 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26331e3864940b9c7f2a2588e3d3cbfa9944c900
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060353"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>指定 Oracle 發行者的資料類型對應
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定 Oracle 發行者的資料類型對應。 雖然有針對 Oracle 發行者提供一組預設的資料類型對應，但是可能需要針對給定的發行集指定不同的對應。  
  
 **本主題內容**  
  
-   **若要指定 Oracle 發行者的資料類型對應，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [發行項**屬性- \<Article> ** ] 對話方塊的 [**資料對應**] 索引標籤上，指定資料類型對應。 您可以從 [新增發行集] 和 [**發行集屬性- \<Publication> ** ] 對話方塊的 [發行項] 頁面取得此**專案**。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[從 Oracle 資料庫建立發行集](create-a-publication-from-an-oracle-database.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-a-data-type-mapping"></a>若要指定資料類型對應  
  
1.  在 [**新增**發行集嚮導] 或 [發行集**屬性 \<Publication> -** ] 對話方塊的 [發行項] 頁面上，選取資料表，然後按一下 [發行項**屬性**]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 [發行**項屬性- \<Article> ** ] 對話方塊的 [**資料對應**] 索引標籤上，從 [**訂閱者資料類型] 資料**行選取對應：  
  
    -   針對某些資料類型，只有一個可能的對應，在此情況下，屬性方格中的資料行為唯讀。  
  
    -   對於某些資料類型，有多種類型可供您選擇。 除非您的應用程式需要不同的對應，否則[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議您使用預設對應。 如需詳細資訊，請參閱 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式指定自訂資料類型對應。 您也可以設定在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 與非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫管理系統（DBMS）之間對應資料類型時，所使用的預設對應。 如需詳細資訊，請參閱 [Data Type Mapping for Oracle Publishers](../non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>在建立屬於 Oracle 發行集的發行項時定義自訂資料類型對應  
  
1.  如果沒有 Oracle 發行集存在，請建立一個。  
  
2.  在散發者上執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **\@use_default_datatypes** 指定 **0** 值。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
3.  在散發者上，執行 [sp_helparticlecolumns](/sql/relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql) ，以檢視已發行之發行項中資料行的現有對應。  
  
4.  在散發者上，執行 [sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)。 指定「 ** \@ 發行者**」的「Oracle 發行者」的名稱，以及「發行集** \@ 」、「** 發行項」和「資料** \@ 行**」來定義已發行的資料行。 ** \@ ** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]針對** \@ 類型**，指定要對應的資料類型名稱，以及** \@ 長度**、有效** \@ 位數和小**數位數（如果適用的話）。 ** \@ **  
  
5.  在散發者上執行 [sp_articleview](/sql/relational-databases/system-stored-procedures/sp-articleview-transact-sql)。 這樣會建立用來從 Oracle 發行集產生快照集的檢視。  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>將對應指定為資料類型的預設對應  
  
1.  (選擇性) 在任何資料庫的散發者上，執行 [sp_getdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql)。 指定** \@ source_dbms**、 ** \@ source_type**、 ** \@ destination_dbms**、 ** \@ destination_version**，以及識別來源 dbms 所需的任何其他參數。 目的地 DBMS 中有關目前對應之資料類型的資訊會使用輸出參數傳回。  
  
2.  (選擇性) 在任何資料庫的散發者上，執行 [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql)。 指定篩選結果集所需的** \@ source_dbms**和任何其他參數。 請記下結果集中所需之對應的 **mapping_id** 值。  
  
3.  在任何資料庫的散發者上，執行 [sp_setdefaultdatatypemapping](/sql/relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql)。  
  
    -   如果您知道步驟 2 中所取得 **mapping_id** 的所需值，請針對 **\@mapping_id** 來指定它。  
  
    -   如果您不知道 **mapping_id**，請指定 **\@source_dbms**、**\@source_type**、**\@destination_dbms**、**\@destination_type** 等參數，以及識別現有對應所需的任何其他參數。  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>在有效的資料類型中找出給定的 Oracle 資料類型  
  
1.  在任何資料庫的散發者上，執行 [sp_helpdatatypemap](/sql/relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql)。 為** \@ Source_dbms**指定**ORACLE**的值，以及篩選結果集所需的任何其他參數。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會變更具有 NUMBER 之 Oracle 資料類型的資料行，好讓它對應到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 `numeric`(38,38)，而不是預設的資料類型 `float`。  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_changecolumndatatype)]  
  
 這個範例查詢會針對 Oracle 9 資料類型 `CHAR` 傳回預設及替代對應。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_char)]  
  
 這個範例查詢會針對 Oracle 9 資料類型 `NUMBER` 傳回預設對應 (如果指定此資料類型，則不含小數位數或有效位數)。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../snippets/tsql/SQL15/replication/howto/tsql/datatypemapping.sql#sp_helpcolumndatatype_number)]  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行者的資料類型對應](../non-sql/data-type-mapping-for-oracle-publishers.md)   
 [異質資料庫複寫](../non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [設定 Oracle 發行者](../non-sql/configure-an-oracle-publisher.md)  
  
  
