---
title: 修改檢查條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c5f6d7acb3827b425b4b3dedb533f33fc0574db4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="modify-check-constraints"></a>修改檢查條件約束
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  當您想要變更條件約束運算式或是針對特定條件啟用或停用條件約束的選項時，可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中修改檢查條件約束。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目來修改檢查條件約束：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>若要修改檢查條件約束  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下包含檢查條件約束的資料表，並選取 [設計]。  
  
2.  在 **[資料表設計工具]** 功能表上，按一下 **[檢查條件約束]**。  
  
3.  在 **[檢查條件約束]** 對話方塊的 **[選取的檢查條件約束]**底下，選取您想要編輯的條件約束。  
  
4.  完成下表中的動作：  
  
    |若要|請依照下列步驟：|  
    |--------|------------------------|  
    |編輯條件約束運算式|在 **[運算式]** 欄位中輸入新的運算式。|  
    |重新命名條件約束|在 **[名稱]** 欄位中輸入新的名稱。|  
    |套用條件約束至現有資料|選取 [ **檢查建立或啟用時的現有資料** ] 選項。|  
    |當加入新資料至資料表，或當現有資料在資料表中更新時，停用條件約束。|清除 [ **INSERT 及 UPDATE 必須合乎條件約束** ] 選項。|  
    |當複寫代理程式在資料表中插入或更新資料時，停用條件約束。|清除 **[強制複寫]** 選項。|  
  
    > [!NOTE]  
    >  某些資料庫具有不同的檢查條件約束功能。  
  
5.  按一下 [ **關閉**]。  
  
6.  在 [檔案]  功能表上，按一下 [儲存 <資料表名稱>]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要修改檢查條件約束**  
  
 若要使用 `CHECK` 來修改 [!INCLUDE[tsql](../../includes/tsql-md.md)]條件約束，您必須先刪除現有的 `CHECK` 條件約束，然後以新的定義重新建立。 如需詳細資訊，請參閱 [Delete Check Constraints](../../relational-databases/tables/delete-check-constraints.md) (刪除檢查條件約束) 和 [Create Check Constraints](../../relational-databases/tables/create-check-constraints.md)(建立檢查條件約束)。  
  
###  <a name="TsqlExample"></a>  
