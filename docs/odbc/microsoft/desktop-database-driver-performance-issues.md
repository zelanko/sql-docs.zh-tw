---
title: 桌面資料庫驅動程式效能問題 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303499"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面資料庫驅動程式效能問題
為了確保與現有 ANSI 應用程式的相容性,SQL_WCHAR、SQL_WVARCHAR 和SQL_WLONGVARCHAR數據類型公開為 Microsoft Access 4.0 或更高數據源SQL_CHAR、SQL_VARCHAR和SQL_LONGVARCHAR。 數據源不返回 WIDE CHAR 資料類型,但數據仍必須以寬字元形式發送到 Jet。 請務必瞭解,如果SQL_C_CHAR參數或結果列綁定到 ANSI 應用程式中的SQL_CHAR數據類型,則轉換將發生。  
  
 當SQL_C_CHAR類型綁定到 LONGVARCHAR 類型的參數時,此轉換在記憶體方面可能特別低效。 由於 Jet 4.0 引擎無法流式傳輸 LONGTEXT 參數數據,因此必須分配一個 UNICODE 轉換緩衝區,該緩衝區的大小是 anSI 緩衝區SQL_C_CHAR兩倍。 最有效的機制是應用程式執行 UNICODE 轉換並將參數綁定為類型SQL_C_WCHAR。 當參數標記為執行數據,並且數據在 SQLPutData 的多次調用中提供時,將創建一個長文本數據緩衝區。 避免增加此"Put Data"緩衝區的費用的一種方法是通過 SQL_DATA_AT_EXEC_LEN(x)提供可選長度,其中*x*是位元組的預期長度。 這將初始化內部 PutData 緩衝區的大小為*x*位元組。  
  
> [!NOTE]  
>  可以使用**SQLBulk 操作()** 或**SQLSetPos()** 將長數據設置為SQL_DATA_AT_EXEC,實現插入或更新長數據的有效方法。 (在這種情況下,EXEC_LEN將被忽略。數據可以通過多次調用**SQLPutData**以區塊進行流式傳輸,這將有效地將數據追加到表中。  
  
 當透過 Microsoft ODBC 桌面資料庫驅動程式使用 Jet 3.5 資料庫的應用程式升級到版本 4.0 時,可能會出現一些性能下降和工作集大小的增加。 這是因為當版本 3 時。*x*資料庫使用新版本 4.0 驅動程式打開,它載入 Jet 4.0。 當 Jet 4.0 打開資料庫,看到資料庫為 3 時。*x*版本,它載入一個可安裝的ISAM驅動程式,相當於載入Jet 3.5引擎。 要消除性能和尺寸損失,請使用 Jet 3。*x*資料庫應壓縮到 Jet 4.0 格式資料庫中。 這將消除載入兩個 Jet 引擎,並最大限度地減少數據的代碼路徑。  
  
 此外,Jet 4.0 發動機是 Unicode 引擎。 所有字串都在 Unicode 中儲存和操作。 當 ANSI 應用程式訪問 Jet 3 時。*x*資料庫透過 Jet 4.0 引擎,數據從 ANSI 轉換為 Unicode 並返回 ANSI。 如果資料庫更新為版本 4.0 格式,字串將轉換為 Unicode,刪除一個級別的字串轉換,並通過僅透過一個 Jet 引擎最小化資料的代碼路徑。
