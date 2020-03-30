---
title: 建立同義字 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- sql13.swb.synonym.general.f1
helpviewer_keywords:
- creating synonyms
- synonyms [SQL Server], creating
ms.assetid: fedfa7a5-d0b6-4e2b-90f4-a08122958e33
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b6ccdce58ca96a26a607996943e6d48d9bac1d8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "72909733"
---
# <a name="create-synonyms"></a>建立同義字
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立同義字。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來建立同義字：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 若要以給定結構描述建立同義字，使用者必須擁有 CREATE SYNONYM 權限，並擁有該結構描述或 ALTER SCHEMA 權限。 CREATE SYNONYM 權限是可授與的權限。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-synonym"></a>若要建立同義字  
  
1.  在 **[物件總管]** 中，展開您要建立新檢視表的資料庫。  
  
2.  以滑鼠右鍵按一下 [同義字]  資料夾，然後按一下 [新增同義字]  。  
  
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
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-synonym"></a>若要建立同義字  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]** 。  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
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
  
  
