---
description: MSSQLSERVER_5009
title: MSSQLSERVER_5009
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5009 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 1ca7fb52969d9ec08d8c80c48ec1325277a13fa7
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418746"
---
# <a name="mssqlserver_5009"></a>MSSQLSERVER_5009
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|5009|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|ALT_BADDISKS|
|訊息文字|找不到陳述式中所列的一或多個檔案，或無法初始化|
||

## <a name="explanation"></a>說明

此錯誤表示您在 ALTER DATABASE 或 DBCC SHRINK* 命令中指定了無法解析的檔案名稱或檔案識別碼。

考慮下列案例：

- 您有一個使用完整或大量記錄復原模式的 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。
- 您會將名為 *db_file1* 的新資料檔案新增至資料庫。
- 您將 `db_file1` 檔案的檔案類型設定為資料。
- 您知道指定的檔案類型不正確。
- 您會移除 `db_file1` 檔案，然後備份此資料庫的交易記錄。
- 您會將名為 *db_file1* 的新記錄檔新增至相同資料庫。
- 您嘗試使用 ALTER DATABASE 陳述式或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio 來移除名為 *db_file1* 的記錄檔。

在此案例中，您會收到類似下列的錯誤訊息：

> 訊息 5009，層級 16，狀態 9，行 1 找不到陳述式中所列的一或多個檔案，或無法初始化。

## <a name="possible-causes"></a>可能的原因

如果嘗試移除的檔案其邏輯名稱在系統目錄資料表中非為唯一，就會發生此問題。 例如，如果檔案先前存在於資料庫中，然後移除了該檔案，就會發生這個問題。

當嘗試移除具有相同邏輯名稱的檔案時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試移除已卸除的邏輯檔案。 這會導致產生錯誤訊息。

## <a name="user-action"></a>使用者動作

若要暫時解決此問題，請依照這些步驟執行。

> [!NOTE]
> 這些步驟會導致重複使用檔案識別碼值。

1. 使用 ALTER DATABASE 陳述式來建立具有不同名稱和相同資料類型的新邏輯檔案。 例如，將邏輯檔案命名為 `different_remove_file_name` 而不是 `db_file1`，如下列範例所示：

    ```sql
    ALTER DATABASE [DBNAME] ADD FILE ( NAME = N'different_remove_file_name',
    FILENAME = N'D:\MSSQL.1\MSSQL\DATA\db_file1.ndf', SIZE = 1MB, MAXSIZE = 1MB)
    ```

    > [!NOTE]
    > 您可使用任何檔案名稱或任何檔案路徑。

1. 使用 ALTER DATABASE 陳述式來移除在步驟 1 中建立的邏輯檔案，如下列範例所示：

    ```sql
    ALTER DATABASE [DBNAME] REMOVE FILE [different_remove_file_name]
    ```

1. 建立資料庫的交易記錄備份。
1. 嘗試再次移除名為 *db_file1* 的邏輯檔案。
