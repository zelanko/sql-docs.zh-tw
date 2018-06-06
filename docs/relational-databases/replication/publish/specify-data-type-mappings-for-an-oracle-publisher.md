---
title: 指定 Oracle 發行者的資料類型對應 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 730525d439da22de116cb4239889720e0256351d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>指定 Oracle 發行者的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定 Oracle 發行者的資料類型對應。 雖然有針對 Oracle 發行者提供一組預設的資料類型對應，但是可能需要針對給定的發行集指定不同的對應。  
  
 **本主題內容**  
  
-   **若要指定 Oracle 發行者的資料類型對應，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [發行項屬性 - \<發行項>] 對話方塊的 [資料對應] 索引標籤上，指定資料類型對應。 您可以從 [新增發行集精靈] 的 [發行項] 頁面，以及 [發行集屬性 - \<發行集>] 對話方塊存取這個對話方塊。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[從 Oracle 資料庫建立發行集](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-a-data-type-mapping"></a>若要指定資料類型對應  
  
1.  在 [新增發行集精靈] 的 [發行項] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊中，選取一個資料表，然後按一下 [發行項屬性]。  
  
2.  按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 [發行項屬性 - \<發行項>] 對話方塊的 [資料對應] 索引標籤上，從 [訂閱者資料類型] 資料行選取對應：  
  
    -   針對某些資料類型，只有一個可能的對應，在此情況下，屬性方格中的資料行為唯讀。  
  
    -   對於某些資料類型，有多種類型可供您選擇。 除非您的應用程式需要不同的對應，否則[!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議您使用預設對應。 如需詳細資訊，請參閱 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式指定自訂資料類型對應。 您也可以設定在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 與非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫管理系統 (DBMS) 之間對應資料類型時，所使用的預設對應。 如需詳細資訊，請參閱 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)。  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>在建立屬於 Oracle 發行集的發行項時定義自訂資料類型對應  
  
1.  如果沒有 Oracle 發行集存在，請建立一個。  
  
2.  在散發者上執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 針對 **@use_default_datatypes** 指定 **@use_default_datatypes**中指定 Oracle 發行者的資料類型對應。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  在散發者上，執行 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) ，以檢視已發行之發行項中資料行的現有對應。  
  
4.  在散發者上，執行 [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)。 針對 **@publisher**指定 Oracle 發行者的名稱，並指定 **@publication**、 **@article**和 **@column** 來定義已發行的資料行。 針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] @type **@type**指定 Oracle 發行者的名稱，並指定 **@length**、 **@precision**和 **@scale**。  
  
5.  在散發者上執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 這樣會建立用來從 Oracle 發行集產生快照集的檢視。  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>將對應指定為資料類型的預設對應  
  
1.  (選擇性) 在任何資料庫的散發者上，執行 [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。 指定 **@source_dbms**、 **@source_type**、 **@destination_dbms**、 **@destination_version**及識別來源 DBMS 所需的任何其他參數。 目的地 DBMS 中有關目前對應之資料類型的資訊會使用輸出參數傳回。  
  
2.  (選擇性) 在任何資料庫的散發者上，執行 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)。 指定 **@source_dbms** 及篩選結果集所需的任何其他參數。 請記下結果集中所需之對應的 **mapping_id** 值。  
  
3.  在任何資料庫的散發者上，執行 [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)。  
  
    -   如果您知道步驟 2 中取得之 **mapping_id** 的所要值，請針對 **@mapping_id**中指定 Oracle 發行者的資料類型對應。  
  
    -   如果您不知道 **mapping_id**，請指定 **@source_dbms**、 **@source_type**、 **@destination_dbms**、 **@destination_type**等參數，以及識別現有對應所需的任何其他參數。  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>在有效的資料類型中找出給定的 Oracle 資料類型  
  
1.  在任何資料庫的散發者上，執行 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)。 針對 **@source_dbms** 指定 **@source_dbms** 及篩選結果集所需的任何其他參數。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會變更具有 NUMBER 之 Oracle 資料類型的資料行，好讓它對應到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **numeric**(38,38)，而不是預設的資料類型 **float**中指定 Oracle 發行者的資料類型對應。  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 這個範例查詢會針對 Oracle 9 資料類型 **CHAR**傳回預設及替代對應。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 這個範例查詢會針對 Oracle 9 資料類型 **NUMBER** 傳回預設對應 (如果指定此資料類型，則不含小數位數或有效位數)。  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [異質資料庫複寫](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  
