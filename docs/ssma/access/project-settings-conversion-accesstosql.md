---
title: "專案設定 （轉換） (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec31bf02ccdeedd4356d0a85c85d7d33041d5bde
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="project-settings-conversion-accesstosql"></a>專案設定 （轉換） (AccessToSQL)
轉換專案設定可讓您設定如何將物件轉換到存取資料庫物件從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件。  
  
[轉換] 窗格位於**專案設定**和**預設專案設定**對話方塊。  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要存取轉換設定在**工具**功能表上，選取**專案設定**，按一下 **一般**底部的左的窗格，然後選取**轉換**。  
  
-   使用**預設專案設定**對話方塊來設定所有專案的組態選項。 若要存取轉換設定在**工具**功能表上，選取**預設專案設定**，選取移轉專案類型設定為需要從變更 / 檢視**移轉的目標版本**下拉式清單中，按一下 **一般**底部的左的窗格，然後選取**轉換**。  
  
## <a name="options"></a>選項  
**新增主索引鍵**  
建立新的主要金鑰中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料表，如果 Access 資料表沒有主索引鍵或唯一索引。  
  
-   **預設模式**: False  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
當連接到 SQL Azure 時，預設為 True。**加入時間戳記資料行**  
指定 SSMA 是否應在必要時建立時間戳記值。  
  
-   **預設模式**： 讓 SSMA 決定  
  
-   **開放式模式**： 從未  
  
-   **完整模式**： 讓 SSMA 決定  
  
**包含與轉換的評估報告的資料評估報告**  
評估報表中包含的資料評估。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
**當主索引鍵包含 null 的資料行的訊息類型**  
指定 SSMA 顯示 [輸出] 窗格中，找到具有可為 null 的資料行的主索引鍵時的訊息 （警告、 錯誤或執行任何動作） 的類型。  
  
-   **預設模式**： 警告  
  
-   **開放式模式**： 沒有任何訊息  
  
-   **完整模式**： 錯誤  
  
**當外部索引鍵資料行的大小不同的訊息類型**  
指定 SSMA 會顯示 [輸出] 窗格中，發現不正確的文字外部索引鍵時的訊息 （警告、 錯誤或執行任何動作） 的類型。  
  
-   **預設模式**： 警告  
  
-   **開放式模式**： 沒有任何訊息  
  
-   **完整模式**： 錯誤  
  
**當備忘資料行索引的訊息類型**  
指定 SSMA 會顯示 [輸出] 窗格中，找到包含的索引時的訊息 （警告、 錯誤或執行任何動作） 的型別**備忘**資料行。  
  
-   **預設模式**： 警告  
  
-   **開放式模式**： 沒有任何訊息  
  
-   **完整模式**： 錯誤  
  
**當複雜查詢中使用萬用字元，就發出警告 (\&#42;)**  
當 SELECT 陳述式中的資料行名稱為萬用字元 （*） 時，請在 輸出 窗格和 錯誤清單中顯示警告。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
**識別項名稱變更時，即發出警告**  
評估報表中與輸出窗格中變更 SSMA 物件識別項名稱時，顯示訊息。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
**將引號識別項時，即發出警告**  
評估報表中與輸出窗格中物件的識別項名稱會加上引號的 SSMA 時，顯示一則訊息。 引號識別項時，所需的名稱是關鍵字，或包含特殊字元。  
  
-   **預設模式**: True  
  
-   **開放式模式**: False  
  
-   **完整模式**: True  
  
## <a name="see-also"></a>另請參閱  
[使用者介面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
