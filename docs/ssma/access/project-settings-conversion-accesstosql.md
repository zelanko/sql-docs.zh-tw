---
title: 專案設定（轉換）（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ff44d34e6c701c8d43260982d3117def4cb9530d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929451"
---
# <a name="project-settings-conversion-accesstosql"></a>專案設定（轉換）（AccessToSQL）
轉換專案設定可讓您設定物件從 Access 資料庫物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫物件的方式。  
  
[轉換] 窗格可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中取得。  
  
-   使用 [**專案設定**] 對話方塊，即可設定目前專案的配置選項。 若要存取轉換設定，請在 [**工具**] 功能表上，選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後選取 [**轉換**]。  
  
-   使用 [**預設專案設定**] 對話方塊，即可設定所有專案的設定選項。 若要存取轉換設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，從 [**遷移目標版本**] 下拉式/changed 選取 [需要查看設定] 的 [遷移專案類型]，按一下左窗格底部的 **[一般**]，然後選取 [**轉換**]。  
  
## <a name="options"></a>選項  
**新增主要金鑰**  
如果 Access 資料表沒有主鍵或唯一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]索引，則在或 SQL Azure 資料表中建立新的主要金鑰。  
  
-   **預設模式**： False  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
連線到 SQL Azure 時，預設為 True。**新增時間戳記資料行**  
指定 SSMA 是否應該在需要時建立時間戳記值。  
  
-   **預設模式**：讓 SSMA 決定  
  
-   **開放式模式**：永不  
  
-   **完整模式**：讓 SSMA 決定  
  
**包含具有轉換評估報告的資料評估報告**  
在評量報告中包含資料評估。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當主鍵包含可為 null 的資料行時的訊息類型**  
指定當發現具有可為 null 之資料行的主鍵時，SSMA 顯示在 [輸出] 窗格中的訊息類型（警告、錯誤或任何內容）。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**當外鍵資料行的大小不同時的訊息類型**  
指定當發現不正確的文字外鍵時，SSMA 顯示在 [輸出] 窗格中的訊息類型（警告、錯誤或任何內容）。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**索引備忘資料行時的訊息類型**  
指定在找到包含**備忘**資料行的索引時，SSMA 顯示在 [輸出] 窗格中的訊息類型（警告、錯誤或任何內容）。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**當複雜查詢使用萬用字元時發出警告（\&#42;)**  
當 SELECT 語句中的資料行名稱為萬用字元（*）時，會在 [輸出] 窗格中顯示警告，並錯誤清單。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當識別碼名稱變更時發出警告**  
當 SSMA 變更物件識別碼名稱時，會在 [評估] 報告和 [輸出] 窗格中顯示一則訊息。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當識別碼會加上引號時發出警告**  
當物件識別碼名稱會以 SSMA 括住時，會在 [評估] 報告和 [輸出] 窗格中顯示一則訊息。 當名稱是關鍵字或包含特殊字元時，必須使用引號括住識別碼。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
## <a name="see-also"></a>另請參閱  
[使用者介面參考（存取）](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
