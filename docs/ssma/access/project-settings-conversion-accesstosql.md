---
description: '專案設定 (轉換)  (AccessToSQL) '
title: 專案設定 (轉換)  (AccessToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 63952d4e46b1c25e49e7f29f8da1e23543232cb7
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988504"
---
# <a name="project-settings-conversion-accesstosql"></a>專案設定 (轉換)  (AccessToSQL) 
轉換專案設定可讓您設定物件從 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 物件的方式。  
  
[轉換] 窗格可在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用。  
  
-   使用 [ **專案設定** ] 對話方塊，即可設定目前專案的設定選項。 若要存取轉換設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後選取 [ **轉換**]。  
  
-   使用 [ **預設專案設定** ] 對話方塊，即可設定所有專案的設定選項。 若要存取轉換設定，請在 [ **工具** ] 功能表上，選取 [ **預設專案設定**]，選取 [從 **遷移目標版本** /changed 需要查看設定的遷移專案類型] 下拉式清單，按一下左窗格底部的 **[一般** ]，然後選取 [ **轉換**]。  
  
## <a name="options"></a>選項  
**新增主要金鑰**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 Access 資料表沒有 primary key 或 unique 索引，則在或 SQL Azure 資料表中建立新的主鍵。  
  
-   **預設模式**： False  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
連線到 SQL Azure 時，預設為 True。**新增時間戳記資料行**  
指定 SSMA 是否應在必要時建立時間戳記值。  
  
-   **預設模式**：讓 SSMA 決定  
  
-   **開放式模式**：永不  
  
-   **完整模式**：讓 SSMA 決定  
  
**包含具有轉換評定報告的資料評量報告**  
在評量報告中包含資料評量。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當主鍵包含可為 null 的資料行時的訊息類型**  
指定當 SSMA 在尋找具有可為 null 之資料行的主鍵時，顯示在 [輸出] 窗格中的訊息類型 (警告、錯誤或 Nothing) 。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**外鍵資料行的大小不同時的訊息類型**  
指定當 SSMA 發現不正確的文字外鍵時，[輸出] 窗格中顯示的訊息類型 (警告、錯誤或 Nothing) 。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**將備忘錄資料行編制索引時的訊息類型**  
指定當 SSMA 在尋找包含 **備忘錄** 資料行的索引時，[輸出] 窗格中顯示的訊息類型 (警告、錯誤或 Nothing) 。  
  
-   **預設模式**：警告  
  
-   **開放式模式**：沒有訊息  
  
-   **完整模式**：錯誤  
  
**當複雜查詢使用萬用字元 (#42; 時發出警告 \& ) **  
當 SELECT 語句中的資料行名稱為萬用字元 ( * ) 時，會在 [輸出] 窗格和 [錯誤清單] 中顯示警告。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當識別碼名稱變更時發出警告**  
當 SSMA 變更物件識別碼名稱時，在評估報告和 [輸出] 窗格中顯示一則訊息。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
**當識別碼會加上引號時發出警告**  
當物件識別碼名稱將以 SSMA 括住時，在評量報告和輸出窗格中顯示訊息。 當名稱是關鍵字或包含特殊字元時，就必須使用引號識別碼。  
  
-   **預設模式**： True  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
## <a name="see-also"></a>另請參閱  
[消費者介面參考 (存取) ](./user-interface-reference-accesstosql.md)  
