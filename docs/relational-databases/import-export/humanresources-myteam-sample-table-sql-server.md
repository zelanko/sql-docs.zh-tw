---
title: HumanResources.myTeam 範例資料表 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a95168f9c932b187a77d0d8e97511fd0070ea8ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035680"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>HumanResources.myTeam 範例資料表 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [匯入和匯出大量資料](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) 中有許多程式碼範例都需要一個特殊用途的測試資料表，此資料表名為 **myTeam**。 執行這些範例前，您必須先在 **資料庫的** HumanResources **結構描述中建立** myTeam [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表。  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的其中一個範例資料庫。  
  
 **myTeam** 資料表包含下列資料行。  
  
|「資料行」|資料類型|Null 屬性|Description|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|非 Null|資料列的主索引鍵。 小組某個成員的員工識別碼。|  
|**名稱**|**nvarchar(50)**|非 Null|小組某個成員的名稱。|  
|**Title**|**nvarchar(50)**|可為 Null|小組中工作的員工之職稱。|  
|**背景**|**nvarchar(50)**|非 Null|資料列上次更新的日期和時間。 (預設值)|  
  
**若要建立 HumanResources.myTeam**  
  
-   使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**若要擴展 HumanResources.myTeam**  
  
-   執行下列 `INSERT` 陳述式，將資料表擴展為兩個資料列：  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  這些陳述式會略過第四個資料行 `Background`。 這有預設值。 略過這個資料行會造成這個 `INSERT` 陳述式將該資料行保留為空白。  
  
## <a name="see-also"></a>另請參閱  
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
