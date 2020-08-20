---
description: 測試移轉的資料庫物件 (SybaseToSQL)
title: 測試遷移的資料庫物件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cfe57d436eac38052542eb2ed6c2133aab7ca07b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480383"
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>測試移轉的資料庫物件 (SybaseToSQL)
Microsoft SQL Server 移轉小幫手適用于 Sybase 測試器 (SSMA 測試器) 自動測試資料庫物件轉換和 SSMA 所進行的資料移轉。 所有 SSMA 的遷移步驟都完成後，請使用 SSMA 測試人員確認轉換的物件以相同方式運作，而且所有資料都已正確傳輸。  
  
> [!NOTE]  
> 在 Azure 連線情況下，會停用測試人員元件。  
  
您可以使用 SSMA 測試人員測試下列物件類型：  
  
-   資料表  
  
-   預存程序  
  
-   檢視。  
  
-   獨立語句。  
  
SSMA 測試人員會執行選取的物件，以便在 Sybase 與其在 SQL Server 中的對應專案上進行測試。 之後，它會根據下列準則來比較結果：  
  
-   資料表資料中的變更是否相同？  
  
-   程式和函式的輸出參數值是否相同？  
  
-   函數會傳回相同的結果嗎？  
  
-   結果集是否相同？  
  
> [!NOTE]  
> 注意！ 請勿在生產系統上使用 SSMA 測試人員。 在測試執行期間，會修改來源架構和資料。 同時，某些類型的測試程式碼可能無法完全還原原始狀態。  
  
## <a name="prerequisites"></a>先決條件  
如果您想要使用 SSMA 測試器，請開啟 [ **安裝測試器資料庫** ] 選項來安裝 SSMA Sybase 擴充功能套件。  
  
此外，請確認下列事項：  
  
-   Sybase OLE DB 提供者安裝在執行的電腦上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   資料庫引擎上已啟用 Common Language Runtime (CLR) 整合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
請注意，目前版本的 SSMA 測試人員不支援相同來源或目標伺服器上的不同使用者進行平行執行。  
  
## <a name="getting-started"></a>開始使用  
[&#40;SybaseToSQL&#41;建立測試案例 ](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[在 SQL Server &#40;SybaseToSQL&#41;上安裝 SSMA 元件 ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[專案設定 &#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
