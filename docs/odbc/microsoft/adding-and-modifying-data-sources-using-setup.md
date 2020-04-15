---
title: 使用設定新增和修改資料來源 ( 1 )微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281408"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>使用安裝程式新增和修改資料來源
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 數據源識別可包含網路庫、伺服器、資料庫和其他屬性的資料路徑 - 在這種情況下,資料來源是 Oracle 資料庫的路徑。 要連接到資料源,驅動程式管理員將檢查 Windows 註冊表中的特定連接資訊。  
  
 ODBC 資料來源管理員創建的註冊表項由 ODBC 驅動程式管理員和 ODBC 驅動程式使用。 此條目包含有關每個數據源及其關聯的驅動程序的資訊。 必須先將數據源連接到數據來源之前,必須將其連接資訊添加到註冊表中。  
  
 要新增與設定資料來源,請使用[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)。 ODBC 管理員更新數據源連接資訊。 新增資料來源時,ODBC 管理員會為您更新註冊表資訊。  
  
### <a name="to-add-a-data-source-for-windows"></a>新增資料來源  
  
1.  打開 ODBC 資料來源管理員。  
  
2.  在 ODBC 數據源管理員對話方塊中,按一下「添加」。 此時將顯示"創建新資料源"對話框。  
  
3.  為 Oracle 選擇 Microsoft ODBC,然後單擊" 完成" 將顯示 Oracle 設定的 Microsoft ODBC 對話方塊。  
  
4.  在「資料源名稱」框中,鍵入要訪問的數據源的名稱。 它可以是您選擇的任何名稱。  
  
5.  在"描述"框中,鍵入驅動程序的說明。 此可選欄位描述數據源連接到的資料庫驅動程式。 它可以是您選擇的任何名稱。  
  
6.  在"使用者名"框中,鍵入資料庫使用者名(資料庫使用者ID)。  
  
7.  在「伺服器」框中,鍵入要存取的 Oracle 伺服器引擎的資料庫別名或連接字串。  
  
8.  按一下「確定」 以添加此數據來源。  
  
> [!NOTE]  
>  將顯示「數據源」對話框,ODBC 管理員將更新註冊表資訊。 當您連接到該資料來源時,您鍵入的使用者名稱和連接字串將成為此資料來源的預設連接值。  
  
1.  點選選項「選項」可針對 Oracle 設定對 ODBC 驅動程式做出更多規格:  
  
    -   **翻譯**- 點擊"選擇"以選擇載入的資料轉換器。 默認值為\<「無翻譯人員>。  
  
    -   **性能**- 目錄函數中的"包含註釋"複選框指定驅動程式是否返回[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果集的備註列。 未設定此值時,Oracle 的 ODBC 驅動程式可提供更快的訪問。  
  
         SQL 列中的「包括 SYNONYMS」複選框指定驅動程式是否返回列資訊。 **緩衝區大小**指定分配給接收提取數據的大小(以位元組為單位)。 驅動程式優化提取,以便從 Oracle 伺服器提取的行返回足夠的行來填充指定大小的緩衝區。 獲取大量數據時,值越大,性能也會提高。  
  
    -   **自定義**- 強制 ODBC DayOfWeek 標準複選框指定結果集是否符合 ODBC 指定的周日格式(周日 = 1;星期六 = 7)。 如果清除此複選框,則返回特定於區域設置的 Oracle 值。  
  
         SQLDescribeCol**始終返回精度值**複選框,指定驅動程式是否應返回**SQLDescribeCol**的*cbColDef*參數的非零值。 此連接字串屬性僅適用於沒有 Oracle 定義比例的欄,例如計算的數位列和定義為 NUMBER 的欄,沒有精度或比例。 當 Oracle 不提供該資訊時 **,SQLDescribeCol**調用返回 130 的精度。 如果清除此複選框,驅動程式將返回這些類型的列 0。  
  
2.  按下「添加」可添加其他數據源,或單擊"關閉以退出」。  
  
### <a name="to-modify-a-data-source-for-windows"></a>變更 Windows 的資料來源  
  
1.  打開 ODBC 資料來源管理員。 按一下相應的 DSN 選項卡。  
  
2.  選擇要修改的 Oracle 資料源,然後單擊「配置」。 將顯示 Oracle 設定的 Microsoft ODBC 對話方塊。  
  
3.  修改適用的資料源欄位,然後單擊"確定"  
  
 完成此對話框中的資訊修改後,ODBC 管理員將更新註冊表資訊。
