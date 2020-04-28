---
title: 測試遷移的資料庫物件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6fb469dfcaaec33a03681bfb64f411851df0400e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020910"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>測試移轉的資料庫物件 (SybaseToSQL)
Sybase 測試器（SSMA 測試器）的 Microsoft SQL Server 移轉小幫手會自動測試資料庫物件轉換和 SSMA 所進行的資料移轉。 完成所有 SSMA 的遷移步驟之後，請使用 SSMA 測試人員來驗證轉換的物件是否以相同的方式運作，以及是否已正確傳輸所有資料。  
  
> [!NOTE]  
> 在 Azure 連線的情況下，會停用測試人員元件。  
  
您可以使用 SSMA 測試器測試下列物件類型：  
  
-   資料表  
  
-   預存程序  
  
-   檢視。  
  
-   獨立語句。  
  
SSMA 測試器會執行選取要在 Sybase 上測試的物件，以及其在 SQL Server 中的對應專案。 之後，它會根據下列準則來比較結果：  
  
-   資料表資料中的變更是否相同？  
  
-   程式和函式的輸出參數值是否相同？  
  
-   函數會傳回相同的結果嗎？  
  
-   結果集是否相同？  
  
> [!NOTE]  
> 加! 絕對不要在生產系統上使用 SSMA 測試器。 在測試器執行期間，會修改來源架構和資料。 同時，針對某些類型的已測試程式碼，完全還原原始狀態是不可能的。  
  
## <a name="prerequisites"></a>Prerequisites  
如果您想要使用 SSMA 測試器，請在開啟 [**安裝測試器資料庫**] 選項的情況下安裝 SSMA Sybase 延伸模組套件。  
  
此外，請確認下列事項：  
  
-   Sybase OLE DB 提供者安裝在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行的電腦上。  
  
-   已在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎上啟用 Common Language RUNTIME （CLR）整合。  
  
請注意，目前版本的 SSMA 測試器不支援由相同來源或目標伺服器上的不同使用者進行平行執行。  
  
## <a name="getting-started"></a>開始使用  
[&#40;SybaseToSQL&#41;建立測試案例](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40;SybaseToSQL 上安裝 SSMA 元件&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[專案設定 &#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
