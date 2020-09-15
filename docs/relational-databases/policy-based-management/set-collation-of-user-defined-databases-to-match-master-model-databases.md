---
title: 設定使用者定義資料庫的定序，使其符合 master 資料庫及模型資料庫
description: 了解如何啟用原則來檢查使用者定義的資料庫和系統資料庫是否具備相同定序。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 905accc62afdc12152110d44a18e61d4c8a9bcef
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284898"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-master-and-model-databases"></a>設定使用者定義資料庫的定序，使其符合 master 資料庫及模型資料庫
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此規則會使用與 master 或 model 定序相同的資料庫定序來定義使用者定義資料庫。
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們建議您最好讓使用者定義資料庫的定序符合 master 或 model 的定序。 否則，可能會發生妨礙程式碼執行的定序衝突。 例如，當預存程序將一個資料表聯結到暫存資料表時，SQL Server 可能會在使用者定義資料庫的定序與 model 資料庫的定序不同時，結束批次並傳回定序衝突錯誤。 發生這個錯誤是因為暫存資料表是在 tempdb 內建立，而 tempdb 的定序是以 model 的定序為根據。

  如果您遇到定序衝突錯誤，請考慮以下其中一個解決方案：

  - 從使用者資料庫將資料匯出到定序與 master 和 model 資料庫相同的新資料表內。

  - 重建系統資料庫，以便使用符合使用者資料庫定序的定序。 如需如何重建系統資料庫的詳細資訊，請參閱[重建系統資料庫](../databases/rebuild-system-databases.md)。

  - 修改可將使用者資料表聯結到 tempdb 內資料表的任何預存程序，以便使用使用者資料庫的定序在 tempdb 中建立資料表。 若要執行這項操作，請將 COLLATE database_default 子句新增到暫存資料表中的資料行定義，如下列範例所示：
  
    ```
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )
    ```

## <a name="see-also"></a>另請參閱
  
 [設定或變更伺服器定序](../collations/set-or-change-the-server-collation.md)  

 [設定或變更資料庫定序](../collations/set-or-change-the-database-collation.md)

 [設定或變更資料行定序](../collations/set-or-change-the-column-collation.md)
 
 [檢視定序資訊](../collations/view-collation-information.md)    
  
  
