---
title: 測試移轉的資料庫物件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 858c564c965fe7105c86a3087923887097e4ddac
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266484"
---
# <a name="testing-migrated-database-objects-oracletosql"></a>測試移轉的資料庫物件 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 軟體測試人員 （SSMA 測試器） 的移轉小幫手會自動測試資料庫物件轉換和 SSMA 所做的資料移轉。 所有 SSMA 的移轉步驟都完成之後，使用 SSMA 軟體測試人員確認已轉換的物件執行相同的方式，而且所有的資料已正確移轉。  
  
使用 SSMA 軟體測試人員，您可以測試下列物件類型：  
  
-   資料表  
  
-   預存程序，包括封裝的程序。  
  
-   使用者定義函式，包括封裝函式。  
  
-   檢視。  
  
-   獨立陳述式。  
  
SSMA 軟體測試人員執行在 Oracle 和其對應項目上進行測試所選取物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在那之後，它會比較的結果，根據下列準則：  
  
-   資料表資料中的變更是否相同？  
  
-   完全相同的程序和函式的輸出參數的值？  
  
-   函式會傳回相同的結果嗎？  
  
-   會將結果集相同嗎？  
  
> [!NOTE]  
> 注意 ！ 絕對不要在實際系統上使用 SSMA 軟體測試人員。 在測試執行期間會修改來源結構描述和資料。 同時，原始狀態的完整還原可能無法針對某些類型的測試的程式碼。  
  
## <a name="prerequisites"></a>先決條件  
如果您想要使用 SSMA Tester，安裝 SSMA Oracle 延伸模組組件，與**安裝的軟體測試人員資料庫**開啟選項。  
  
若要讓產生的資料表資料的比較，請設定**產生 ROWID 資料行**選項設定為**是**結構描述轉換開始前。 SSMA 會新增至所有資料表 ROWID 資料行執行期間**轉換的結構描述**命令。  
  
此外，請檢查下列各項：  
  
-   電腦上安裝 oracle 用戶端工具，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行。  
  
-   已啟用 common Language Runtime (CLR) 整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Database Engine。  
  
請注意，目前版本的 SSMA Tester 不支援平行執行不同的使用者在相同的來源或目標伺服器上。  
  
## <a name="getting-started"></a>使用者入門  
[建立測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 上安裝 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[專案設定&#40;轉換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
