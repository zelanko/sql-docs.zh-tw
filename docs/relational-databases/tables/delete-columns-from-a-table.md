---
title: 從資料表中刪除資料行 | Microsoft 文件
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0db1834114a8bb2ea21d9fb566f2201dd933803c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68088460"
---
# <a name="delete-columns-from-a-table"></a>從資料表中刪除資料行

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除資料表資料行。

> [!CAUTION]
> 當您從資料表中刪除資料行時，會刪除其本身及其其所包含的所有資料。

 **本主題內容**

- **開始之前：**

   [限制事項](#Restrictions)

   [安全性](#Security)

- **若要使用下列項目從資料表中刪除資料行：**

   [Transact-SQL](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項

您無法刪除具有 CHECK 條件約束的資料行。 您必須先刪除條件約束。

除非使用資料表設計工具，否則您無法刪除具有 PRIMARY KEY 或 FOREIGN KEY 條件約束或其他相依性的資料行。 使用 [物件總管] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]時，您必須先移除資料行的所有相依性。

### <a name="security"></a><a name="Security"></a> Security

#### <a name="permissions"></a><a name="Permissions"></a> 權限

需要資料表的 ALTER 權限。

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio

### <a name="to-delete-columns-by-using-object-explorer"></a>若要使用物件總管來刪除資料行

1. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。
2. 在 [物件總管]  中，尋找您想要從中刪除資料行的資料表，然後展開以公開資料行名稱。
3. 以滑鼠右鍵按一下您想要刪除的資料行，然後選擇 [刪除]  。
4. 在 **[刪除物件]** 對話方塊中，按一下 **[確定]** 。

如果資料行包含條件約束或其他相依性， **[刪除物件]** 對話方塊將會顯示錯誤訊息。 請刪除參考的條件約束，藉以解決此錯誤。

### <a name="to-delete-columns-by-using-table-designer"></a>若要使用資料表設計工具來刪除資料行

1. 在**物件總管**中，以滑鼠右鍵按一下您想要從中刪除資料行的資料表，然後選擇 [設計]  。
2. 以滑鼠右鍵按一下您想要刪除的資料行，然後從捷徑功能表中選擇 [刪除資料行]  。
3. 如果資料行參與關聯性 (FOREIGN KEY 或 PRIMARY KEY)，則會有訊息提示您確認是否要刪除選取的資料行及其關聯性。 選擇 [是]  。

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL

### <a name="to-delete-columns"></a>若要刪除資料行

下列範例會示範如何刪除資料行。

```sql
ALTER TABLE dbo.doc_exb DROP COLUMN column_b;
```

如果資料行包含條件約束或其他相依性，將會傳回錯誤訊息。 請刪除參考的條件約束，藉以解決此錯誤。

如需其他範例，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。

## <a name="FollowUp"></a>
