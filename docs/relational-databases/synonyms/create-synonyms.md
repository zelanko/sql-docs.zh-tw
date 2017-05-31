---
title: "建立同義字 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- sql13.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a3180e86333a329e2f86a45f2728630ce6cf526
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="create-synonyms"></a>建立同義字
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立同義字。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來建立同義字：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 若要以給定結構描述建立同義字，使用者必須擁有 CREATE SYNONYM 權限，並擁有該結構描述或 ALTER SCHEMA 權限。 CREATE SYNONYM 權限是可授與的權限。  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-synonym"></a>若要建立同義字  
  
1.  在 **[物件總管]**中，展開您要建立新檢視表的資料庫。  
  
2.  以滑鼠右鍵按一下 [同義字] 資料夾，然後按一下 [新增同義字]。  
  
3.  在 **[加入新的同義字]** 對話方塊中，輸入下列資訊。  
  
     **同義字名稱**  
     輸入用於此物件的新名稱。  
  
     **同義字結構描述**  
     輸入用於此物件之新名稱的結構描述。  
  
     **伺服器名稱**  
     輸入要連接的伺服器執行個體。  
  
     **資料庫名稱**  
     輸入或選取含有物件的資料庫。  
  
     **結構描述**  
     輸入或選取擁有物件的結構描述。  
  
     **物件類型**  
     選取物件的類型。  
  
     **物件名稱**  
     輸入同義字所參考之物件的名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-synonym"></a>若要建立同義字  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會針對 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的現有資料表建立同義字。 然後，此同義字將用於後續範例中。  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyAddressType  
FOR AdventureWorks2012.Person.AddressType;  
GO  
```  
  
 下列範例將在 `MyAddressType` 同義字所參考的基底資料表中插入一列。  
  
```  
USE tempdb;  
GO  
INSERT INTO MyAddressType (Name)  
VALUES ('Test');  
GO  
```  
  
 下列範例示範如何在動態 SQL 中參考同義字。  
  
```  
USE tempdb;  
GO  
EXECUTE ('SELECT Name FROM MyAddressType');  
GO  
```  
  
  
