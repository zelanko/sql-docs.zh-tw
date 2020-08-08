---
title: 測試遷移的資料庫物件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 9e7c63986cde88c7a1ccbf67f8dd3751bb6d41b0
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932829"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>測試移轉的資料庫物件 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 Oracle 測試人員 (SSMA 測試器) 會自動測試資料庫物件轉換和 SSMA 所進行的資料移轉。 完成所有 SSMA 的遷移步驟之後，請使用 SSMA 測試人員來驗證轉換的物件是否以相同的方式運作，以及是否已正確傳輸所有資料。  
  
您可以使用 SSMA 測試器測試下列物件類型：  
  
-   資料表  
  
-   預存程式，包括封裝的程式。  
  
-   使用者定義的函式，包括已封裝的函式。  
  
-   檢視。  
  
-   獨立語句。  
  
SSMA 測試人員會執行選取要在 Oracle 上測試的物件及其在中的對應專案 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 之後，它會根據下列準則來比較結果：  
  
-   資料表資料中的變更是否相同？  
  
-   程式和函式的輸出參數值是否相同？  
  
-   函數會傳回相同的結果嗎？  
  
-   結果集是否相同？  
  
> [!NOTE]  
> 注意！ 絕對不要在生產系統上使用 SSMA 測試器。 在測試器執行期間，會修改來源架構和資料。 同時，針對某些類型的已測試程式碼，完全還原原始狀態是不可能的。  
  
## <a name="prerequisites"></a>必要條件  
如果您想要使用 SSMA 測試器，請在開啟 [**安裝測試器資料庫**] 選項的情況下安裝 SSMA Oracle 延伸模組套件。  
  
若要啟用產生之資料表資料的比較，請在架構轉換開始之前，將 [**產生 ROWID 資料行**] 選項設定為 **[是]** 。 SSMA 會在**轉換架構**命令執行期間，將 ROWID 資料行加入至所有資料表。  
  
此外，請確認下列事項：  
  
-   Oracle 用戶端工具會安裝在執行的電腦上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   已在資料庫引擎上啟用 Common Language Runtime (CLR) 整合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
請注意，目前版本的 SSMA 測試器不支援由相同來源或目標伺服器上的不同使用者進行平行執行。  
  
## <a name="getting-started"></a>開始使用  
[&#40;OracleToSQL&#41;建立測試案例](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40;OracleToSQL 上安裝 SSMA 元件&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[專案設定 &#40;轉換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
