---
description: 刪除檢視
title: 刪除檢視 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4616d7224ab7697eebdca78e935c96521ccedd3d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125051"
---
# <a name="delete-views"></a>刪除檢視
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  您可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中刪除 (卸除) 檢視，方法是使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法，從資料庫刪除檢視：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   當您卸除檢視時，也會從系統目錄中刪除檢視的定義和檢視的其他相關資訊。 檢視的所有權限也都會刪除。  
  
-   在利用 `DROP TABLE` 來卸除的資料表中，您必須利用 `DROP VIEW`來明確卸除任何檢視。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 SCHEMA 的 ALTER 權限或 OBJECT 的 CONTROL 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>若要從資料庫刪除檢視  
  
1.  在 **[物件總管]** 中，展開資料庫，此資料庫包含您要刪除的檢視，然後展開 **[檢視]** 資料夾。  
  
2.  以滑鼠右鍵按一下您要刪除的檢視，然後按一下 [刪除]。  
  
3.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]** 。  
  
    > [!IMPORTANT]  
    >  在 [刪除物件] 對話方塊中按一下 [顯示相依性]，開啟 [_view\_name_ 相依性] 對話方塊。 這就會顯示相依於檢視的所有物件以及檢視所相依的所有物件。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>若要從資料庫刪除檢視  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例只在指定的檢視已存在時才會予以刪除。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)。  
  
  
