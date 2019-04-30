---
title: 專案設定 （轉換） (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2489442eb8de9d8d0ebfb5d8ed902dd2792e22f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299147"
---
# <a name="project-settings-conversion-accesstosql"></a>專案設定 （轉換） (AccessToSQL)
轉換專案設定可讓您設定如何將物件轉換至 Access 資料庫物件從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫物件。  
  
[轉換] 窗格位於**專案設定**並**預設專案設定**對話方塊。  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要存取轉換設定] 中，在**工具**功能表上，選取**專案設定**，按一下 [**一般**在底部的左的窗格中，然後選取**轉換**。  
  
-   使用**預設專案設定**對話方塊來設定的所有專案的組態選項。 若要存取轉換設定] 中，在**工具**功能表上，選取**預設專案設定**，選取 [移轉專案類型，則需要檢視 / 變更設定**移轉目標版本**下拉式清單中，按一下**一般**底部的左的窗格中，然後選取**轉換**。  
  
## <a name="options"></a>選項。  
**加入主索引鍵**  
建立新的主索引鍵中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料表，如果 Access 資料表沒有主索引鍵或唯一索引。  
  
-   **預設模式**:False  
  
-   **開放式模式**:False  
  
-   **完整模式**:True  
  
當連接到 SQL Azure，這是預設為 True。**新增時間戳記資料行**  
指定 SSMA 是否應該在必要時建立時間戳記值。  
  
-   **預設模式**:讓決定的 SSMA  
  
-   **開放式模式**:永不  
  
-   **完整模式**:讓決定的 SSMA  
  
**包括轉換評定報表的資料評估報告**  
評估報表中包含的資料評估。  
  
-   **預設模式**:True  
  
-   **開放式模式**:False  
  
-   **完整模式**:True  
  
**主索引鍵包含可為 null 的資料行時，會產生訊息類型。**  
指定 SSMA 會顯示在 [輸出] 窗格中，找到具有可為 null 的資料行的主索引鍵時的訊息 （警告、 錯誤或執行任何動作） 的類型。  
  
-   **預設模式**:警告  
  
-   **開放式模式**:沒有訊息  
  
-   **完整模式**:錯誤  
  
**當外部索引鍵資料行的不同大小的訊息類型**  
指定 SSMA 會顯示在 [輸出] 窗格中，找到不正確的文字外部索引鍵時的訊息 （警告、 錯誤或執行任何動作） 的類型。  
  
-   **預設模式**:警告  
  
-   **開放式模式**:沒有訊息  
  
-   **完整模式**:錯誤  
  
**備忘錄資料行編製索引時，會產生訊息類型。**  
指定 SSMA 會顯示在 [輸出] 窗格中，找到包含的索引時的訊息 （警告、 錯誤或執行任何動作） 的型別**備忘**資料行。  
  
-   **預設模式**:警告  
  
-   **開放式模式**:沒有訊息  
  
-   **完整模式**:錯誤  
  
**當複雜查詢中使用萬用字元，即發出警告 (\&#42;)**  
SELECT 陳述式中的資料行名稱為萬用字元 （*） 時，請在 輸出 窗格和 錯誤清單中顯示警告。  
  
-   **預設模式**:True  
  
-   **開放式模式**:False  
  
-   **完整模式**:True  
  
**識別項名稱變更時，即發出警告**  
在評估報告和 [輸出] 窗格中的 SSMA 變更物件的識別項名稱，顯示的訊息。  
  
-   **預設模式**:True  
  
-   **開放式模式**:False  
  
-   **完整模式**:True  
  
**加上引號的識別項時發出警告**  
在評估報告和 [輸出] 窗格中時 SSMA 會加上引號的物件識別項名稱，顯示一則訊息。 引號識別項時，所需的名稱是關鍵字，或包含特殊字元。  
  
-   **預設模式**:True  
  
-   **開放式模式**:False  
  
-   **完整模式**:True  
  
## <a name="see-also"></a>另請參閱  
[使用者介面 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
