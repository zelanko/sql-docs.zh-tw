---
title: "將資料行新增至資料表 (資料庫引擎) | Microsoft Docs"
ms.custom: 
ms.date: 10/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserting columns
- columns [SQL Server], adding
- adding columns
ms.assetid: abeb8d52-d562-4e29-9e1e-2923ae874859
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: bc2034ac69dee1a72429e94841aec1763703de7c
ms.openlocfilehash: 82d9586bdd3dce6f463f9c142b4e0a1e9ddb3a72
ms.contentlocale: zh-tw
ms.lasthandoff: 06/05/2017

---
# <a name="add-columns-to-a-table-database-engine"></a>將資料行加入資料表 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

 > 如需舊版 SQL Server 的相關內容，請參閱[將資料行新增至資料表 (資料庫引擎)](https://msdn.microsoft.com/en-US/library/ms190238(SQL.120).aspx)。


  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中將新的資料行加入至資料表。  

  ##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 如果您使用 ALTER TABLE 陳述式，將資料行加入至資料表，系統就會自動將這些資料行加入至資料表的結尾。 如果您想要讓資料行按照特定順序列在資料表中，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 不過，請注意，這並非資料庫設計最佳作法。 最佳作法是在應用程式和查詢層級指定傳回資料行的順序。 您不應該仰賴使用 SELECT *，根據資料表中定義資料行的順序，按照預期的順序傳回所有資料行。 請務必按照您想要顯示資料行的順序，在查詢和應用程式中依名稱指定資料行。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-insert-columns-into-a-table-with-table-designer"></a>若要使用資料表設計工具將資料行插入資料表中  
  
1.  在物件總管 中，以滑鼠右鍵按一下要加入資料行的資料表，然後選擇 [設計]。  
  
2.  在 **[資料行名稱]** 資料行中，按一下第一個空白資料格。  
  
3.  在資料格中輸入資料行名稱。 資料行名稱為必要值。  
  
4.  按下 TAB 鍵以移至 [ **資料類型** ] 資料格，然後從下拉式清單中選取資料類型。 此為必要值。若未加以選擇，將會指派預設值。  
  
    > [!NOTE]  
    >  您可以在 [資料庫工具] 的 [選項] 對話方塊中變更預設值。  
  
5.  在 [ **資料行屬性** ] 索引標籤中繼續定義其他任何的資料行屬性。  
  
    > [!NOTE]  
    >  資料行屬性的預設值會在您建立新資料行時加入，但是您可以在 [資料行屬性] 索引標籤中變更預設值。  
  
6.  新增資料行之後，請從 [檔案] 功能表中，選擇 [儲存**資料表**] 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-insert-columns-into-a-table"></a>若要將資料行插入資料表中  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  下列範例會將兩個資料行加入至 `dbo.doc_exa`資料表。 將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
```  
ALTER TABLE dbo.doc_exa ADD column_b VARCHAR(20) NULL, column_c INT NULL ;  
```  
  
####  <a name="FollowUp"></a> 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  

