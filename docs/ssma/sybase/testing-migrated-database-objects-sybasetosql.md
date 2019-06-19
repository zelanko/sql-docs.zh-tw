---
title: 測試移轉的資料庫物件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e29fac8b9cdb955ddaff6643eacae352e9c39bf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63214302"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>測試移轉的資料庫物件 (SybaseToSQL)
Microsoft SQL Server Migration Assistant for Sybase Tester （SSMA 測試器） 會自動測試資料庫物件轉換和 SSMA 所做的資料移轉。 所有 SSMA 的移轉步驟都完成之後，使用 SSMA 軟體測試人員確認已轉換的物件執行相同的方式，而且所有的資料已正確移轉。  
  
> [!NOTE]  
> 在 Azure 連線能力的情況下，測試人員元件已停用。  
  
使用 SSMA 軟體測試人員，您可以測試下列物件類型：  
  
-   資料表  
  
-   預存程序  
  
-   檢視。  
  
-   獨立陳述式。  
  
SSMA 軟體測試人員執行在 Sybase 和 SQL Server 中的其對應項目上進行測試所選取的物件。 在那之後，它會比較的結果，根據下列準則：  
  
-   資料表資料中的變更是否相同？  
  
-   完全相同的程序和函式的輸出參數的值？  
  
-   函式會傳回相同的結果嗎？  
  
-   會將結果集相同嗎？  
  
> [!NOTE]  
> 注意 ！ 絕對不要在實際系統上使用 SSMA 軟體測試人員。 在測試執行期間會修改來源結構描述和資料。 同時，原始狀態的完整還原可能無法針對某些類型的測試的程式碼。  
  
## <a name="prerequisites"></a>先決條件  
如果您想要使用 SSMA Tester，安裝 SSMA Sybase 延伸模組套件，與**安裝的軟體測試人員資料庫**開啟選項。  
  
此外，請檢查下列各項：  
  
-   Sybase OLE DB 提供者安裝在電腦上其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行。  
  
-   已啟用 common Language Runtime (CLR) 整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Database Engine。  
  
請注意，目前版本的 SSMA Tester 不支援平行執行不同的使用者在相同的來源或目標伺服器上。  
  
## <a name="getting-started"></a>使用者入門  
[建立測試案例&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[SQL Server 上安裝 SSMA 元件&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[專案設定&#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
