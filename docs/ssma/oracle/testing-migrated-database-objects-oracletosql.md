---
title: 測試移轉的資料庫物件 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f03ef5e1-66e6-4c84-ada2-252dd5ada82f
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: da2327f94062d81a9b80e1884deb5150be494faa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-oracletosql"></a>測試移轉的資料庫物件 (OracleToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 適用於 Oracle 軟體測試人員 （SSMA 軟體測試人員） 的移轉小幫手會自動測試轉換資料庫物件和所做的 SSMA 資料移轉。 所有 SSMA 的移轉步驟都完成之後，請確認已轉換的物件運作的方式相同，而且已正確地傳送的所有資料使用 SSMA 軟體測試人員。  
  
您可以使用 SSMA Tester 來測試下列物件類型：  
  
-   資料表  
  
-   預存程序，包括封裝程序。  
  
-   使用者定義函數，包括封裝函式。  
  
-   檢視。  
  
-   獨立陳述式。  
  
SSMA 軟體測試人員執行測試 Oracle 和其對應項目上選取物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在這之後，它會比較的結果，根據下列準則：  
  
-   資料表資料中的變更是否相同？  
  
-   完全相同的程序和函數的輸出參數的值嗎？  
  
-   函式會傳回相同的結果嗎？  
  
-   會將結果集相同嗎？  
  
> [!NOTE]  
> 注意 ！ 絕對不要使用實際系統上的 SSMA 軟體測試人員。 測試人員執行期間會修改來源結構描述和資料。 同時，可能無法針對部分類型的測試的程式碼的完整還原為原始狀態。  
  
## <a name="prerequisites"></a>필수 구성 요소  
如果您想要使用 SSMA Tester，安裝 SSMA Oracle 延伸模組組件與**安裝軟體測試人員資料庫**選項開啟。  
  
若要啟用所產生的資料表資料的比較，設定**產生 ROWID 資料行**選項設定為**是**啟動結構描述轉換之前。 SSMA 會將所有資料表加入 ROWID 資料行執行期間**轉換結構描述**命令。  
  
此外，請確認下列各項：  
  
-   在電腦上安裝 oracle 用戶端工具其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行。  
  
-   上已啟用 common Language Runtime (CLR) 整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Database Engine。  
  
請注意，目前版本的 SSMA Tester 不支援平行執行由不同使用者在相同的來源或目標伺服器上。  
  
## <a name="getting-started"></a>快速入門  
[建立測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/creating-test-cases-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 上的 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[專案設定&#40;轉換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
