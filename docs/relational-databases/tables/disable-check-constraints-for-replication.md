---
title: "停用複寫的檢查條件約束 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
caps.latest.revision: "19"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 432f3190da0556a78f5f434b73b603375e4b037f
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="disable-check-constraints-for-replication"></a>停用複寫的檢查條件約束
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用檢查條件約束。 您也可以明確停用複製的檢查條件約束，當您從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行資料時，這會相當實用。  
  
> [!NOTE]  
>  如果使用複寫發行資料表，則會自動停用複製代理程式所執行作業的檢查條件約束。 當複寫代理程式在訂閱者端執行插入、更新或刪除時，不會檢查條件約束；如果使用者執行插入、更新或刪除，則會檢查條件約束。 停用複製代理程式的條件約束，是因為原本插入、更新或刪除資料時，就已在發行者端檢查過條件約束。 如需詳細資訊，請參閱 [指定結構描述選項](../../relational-databases/replication/publish/specify-schema-options.md)。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>若要停用複製的檢查條件約束  
  
1.  在 **[物件總管]**中，展開包含您要修改之檢查條件約束的資料表，然後展開 **[條件約束]** 資料夾。  
  
2.  以滑鼠右鍵按一下您要修改的檢查條件約束，然後按一下 **[修改]**。  
  
3.  在 **[檢查條件約束]** 對話方塊中的 **[資料表設計工具]**底下，針對 **[強制複寫]** 選取 **[否]**值。  
  
4.  按一下 [ **關閉**]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>若要停用複製的檢查條件約束  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會建立包含 IDENTITY 資料行及 CHECK 條件約束的資料表。 接著範例會卸除條件約束再重新建立，並指定 NOT FOR REPLICATION 子句。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>另請參閱  
 [指定結構描述選項](../../relational-databases/replication/publish/specify-schema-options.md)  
  
  
