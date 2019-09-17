---
title: 建立資料庫主要金鑰 | Microsoft 文件
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 757b6c62d63da2b8f1fa33e5d704d7a2c4fabd38
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978373"
---
# <a name="create-a-database-master-key"></a>建立資料庫主要金鑰

本主題描述如何使用`master` [!INCLUDE[tsql](../../../includes/tsql-md.md)]，在中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]建立資料庫的資料庫主要金鑰。

**本主題內容**

- **開始之前：**

  [安全性](#Security)

- [若要使用 Transact-SQL 建立資料庫主要金鑰](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> 開始之前

### <a name="Security"></a> 安全性

#### <a name="Permissions"></a> 權限

需要資料庫的 CONTROL 權限。

## <a name="TsqlProcedure"></a> 使用 Transact-SQL

### <a name="to-create-a-database-master-key"></a>若要建立資料庫主要金鑰

1. 選擇密碼以加密即將儲存於資料庫的主要金鑰副本。
2. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。
3. 展開 [**系統資料庫**]，以`master`滑鼠右鍵按一下，然後按一下 [追加**查詢**]。
4. 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)。
