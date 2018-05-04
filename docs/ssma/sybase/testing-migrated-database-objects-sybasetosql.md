---
title: 測試移轉的資料庫物件 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d66b93de265c4976c1c570de7cffe828c7424ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>測試移轉的資料庫物件 (SybaseToSQL)
Microsoft SQL Server 移轉小幫手 Sybase 軟體測試人員 （SSMA 軟體測試人員） 的自動測試轉換資料庫物件和所做的 SSMA 資料移轉。 所有 SSMA 的移轉步驟都完成之後，請確認已轉換的物件運作的方式相同，而且已正確地傳送的所有資料使用 SSMA 軟體測試人員。  
  
> [!NOTE]  
> 在 Azure 的連線能力的情況下，測試人員元件會停用。  
  
您可以使用 SSMA Tester 來測試下列物件類型：  
  
-   資料表  
  
-   預存程序  
  
-   檢視。  
  
-   獨立陳述式。  
  
SSMA 軟體測試人員執行測試 Sybase 和 SQL Server 中的與其對應項目上選取的物件。 在這之後，它會比較的結果，根據下列準則：  
  
-   資料表資料中的變更是否相同？  
  
-   完全相同的程序和函數的輸出參數的值嗎？  
  
-   函式會傳回相同的結果嗎？  
  
-   會將結果集相同嗎？  
  
> [!NOTE]  
> 注意 ！ 絕對不要使用實際系統上的 SSMA 軟體測試人員。 測試人員執行期間會修改來源結構描述和資料。 同時，可能無法針對部分類型的測試的程式碼的完整還原為原始狀態。  
  
## <a name="prerequisites"></a>필수 구성 요소  
如果您想要使用 SSMA Tester，安裝 SSMA Sybase 延伸模組組件**安裝軟體測試人員資料庫**選項開啟。  
  
此外，請確認下列各項：  
  
-   Sybase OLE DB 提供者安裝在電腦上其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行。  
  
-   上已啟用 common Language Runtime (CLR) 整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Database Engine。  
  
請注意，目前版本的 SSMA Tester 不支援平行執行由不同使用者在相同的來源或目標伺服器上。  
  
## <a name="getting-started"></a>快速入門  
[建立測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[安裝 SQL Server 上的 SSMA 元件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[專案設定&#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
