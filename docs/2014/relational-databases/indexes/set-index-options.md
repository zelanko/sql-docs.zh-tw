---
title: 設定索引選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- ALLOW_ROW_LOCKS option
- SORT_IN_TEMPDB option
- DROP_EXISTING clause
- large data, indexes
- PAD_INDEX
- STATISTICS_NORECOMPUTE
- MAXDOP index option, setting
- index options [SQL Server]
- MAXDOP index option
- IGNORE_DUP_KEY option
- ALLOW_PAGE_LOCKS option
- ONLINE
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9f2d7f0bbbf0d152d3f510ae9ddbe3168634ef96
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049815"
---
# <a name="set-index-options"></a>設定索引選項
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改索引的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法修改索引的屬性：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   透過使用 ALTER INDEX 陳述式的 SET 子句，會在索引立即套用下列選項：ALLOW_PAGE_LOCKS、ALLOW_ROW_LOCKS、IGNORE_DUP_KEY 和 STATISTICS_NORECOMPUTE。  
  
-   當您使用 ALTER INDEX REBUILD 或 CREATE INDEX WITH DROP_EXISTING 重建索引時，可以設定下列選項：PAD_INDEX、FILLFACTOR、SORT_IN_TEMPDB、IGNORE_DUP_KEY、STATISTICS_NORECOMPUTE、ONLINE、ALLOW_ROW_LOCKS、ALLOW_PAGE_LOCKS、MAXDOP 和 DROP_EXISTING (僅限 CREATE INDEX)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-properties-of-an-index-in-table-designer"></a>在資料表設計工具中修改索引的屬性  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要修改索引屬性的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下要修改索引屬性的資料表，然後選取 [設計]  。  
  
4.  在 [資料表設計工具]  功能表上，按一下 [索引/索引鍵]  。  
  
5.  選取您要修改的索引。 其屬性會在主要方格中顯示。  
  
6.  變更任何和所有屬性的設定，以自訂索引。  
  
7.  按一下 [關閉]  。  
  
8.  在 [檔案]  功能表上，選取 [儲存 _table_name_]  。  
  
#### <a name="to-modify-the-properties-of-an-index-in-object-explorer"></a>在物件總管中修改索引的屬性  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要修改索引屬性的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要修改索引屬性的資料表。  
  
4.  按一下加號展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下要修改其屬性的索引，然後選取 [屬性]  。  
  
6.  在 **[選取頁面]** 底下，選取 **[選項]** 。  
  
7.  變更任何和所有屬性的設定，以自訂索引。  
  
8.  若要新增、移除或變更索引資料行的位置，請選取 [索引屬性 - _index_name_]  對話方塊中的 [一般]  頁面。 如需相關資訊，請參閱 [Index Properties F1 Help](index-properties-f1-help.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-see-the-properties-of-all-the-indexes-in-a-table"></a>查看資料表中所有索引的屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT i.name AS index_name,   
        i.type_desc,   
        i.is_unique,   
        ds.type_desc AS filegroup_or_partition_scheme,   
        ds.name AS filegroup_or_partition_scheme_name,   
        i.ignore_dup_key,   
        i.is_primary_key,   
        i.is_unique_constraint,   
        i.fill_factor,   
        i.is_padded,   
        i.is_disabled,   
        i.allow_row_locks,   
        i.allow_page_locks,   
        i.has_filter,   
        i.filter_definition  
    FROM sys.indexes AS i  
       INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
    WHERE is_hypothetical = 0 AND i.index_id <> 0   
       AND i.object_id = OBJECT_ID('HumanResources.Employee');   
    GO  
  
    ```  
  
#### <a name="to-set-the-properties-of-an-index"></a>設定索引的屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]** 。  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)。  
  
  
