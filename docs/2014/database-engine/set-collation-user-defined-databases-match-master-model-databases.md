---
title: 設定使用者定義資料庫的定序，使其符合 master 和 model 資料庫的定序 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfb00b1cc1a9930f7a374403b40e2c0d793eb090
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62773307"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>將使用者定義資料庫的定序設定為 master 和 model 資料庫的定序
  此規則會使用與 master 或 model 定序相同的資料庫定序來定義使用者定義資料庫。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們建議您最好讓使用者定義資料庫的定序符合 master 或 model 的定序。 否則，可能會發生妨礙程式碼執行的定序衝突。 例如，當預存程序將一個資料表聯結到暫存資料表時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可能會在使用者定義資料庫的定序與 model 資料庫的定序不同時，結束批次並傳回定序衝突錯誤。 發生這個錯誤是因為暫存資料表是在 tempdb 內建立，而 tempdb 的定序是以 model 的定序為根據。  
  
 如果您遇到定序衝突錯誤，請考慮以下其中一個解決方案：  
  
-   從使用者資料庫將資料匯出到定序與 master 和 model 資料庫相同的新資料表內。  
  
-   重建系統資料庫，以便使用符合使用者資料庫定序的定序。 如需有關如何重建系統資料庫的詳細資訊，請參閱[重建系統資料庫](../relational-databases/databases/system-databases.md)。  
  
-   修改可將使用者資料表聯結到 tempdb 內資料表的任何預存程序，以便使用使用者資料庫的定序在 tempdb 中建立資料表。 若要這樣做，請將 `COLLATE database_default` 子句加入到暫存資料表的資料行定義中，如下列範例所示：  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>詳細資訊  
 [設定或變更資料庫定序](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [設定或變更資料行定序](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Microsoft 知識庫文章325335](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [如何：從命令提示字元安裝 SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
