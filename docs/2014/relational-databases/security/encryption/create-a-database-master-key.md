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
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 86f74710e99079d0acd28db09bcf1e4ba7c57865
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957242"
---
# <a name="create-a-database-master-key"></a>建立資料庫主要金鑰

本主題描述如何使用`master` [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)]，在中建立資料庫的資料庫主要金鑰。

**本主題中的**

- **開始之前：**

  [安全級](#Security)

- [若要使用 Transact-sql 建立資料庫主要金鑰](#TsqlProcedure)

## <a name="BeforeYouBegin"></a>開始之前

### <a name="Security"></a>安全級

#### <a name="Permissions"></a>無權

需要資料庫的 CONTROL 權限。

## <a name="TsqlProcedure"></a>使用 Transact-sql

### <a name="to-create-a-database-master-key"></a>若要建立資料庫主要金鑰

1. 選擇密碼以加密即將儲存於資料庫的主要金鑰副本。
2. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。
3. 展開 [系統資料庫]****，以滑鼠右鍵按一下 `master`，然後按一下 [新增查詢]****。
4. 將下列範例複製並貼入查詢視窗中，然後按一下 [**執行**]。

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)。
