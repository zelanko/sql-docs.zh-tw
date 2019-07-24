---
title: 此 Driver for SQL Server 版本的已知問題 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3508277502ad7e3eb3b0e7ff048301c8ed1efdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008777"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>此驅動程式版本的已知問題

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Microsoft ODBC Driver for SQL Server on Linux and macOS 13、13.1 和 17 版的已知問題清單。

其他問題會公佈於 [Microsoft ODBC 驅動程式團隊部落格](https://blogs.msdn.com/b/sqlnativeclient/)上。  

- Windows、Linux 和 macOS 可能會以不同的方式轉換來自專用區 (PUA) 或使用者定義字元 (EUDC) 的字元。 透過 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在伺服器上執行的轉換，會使用 Windows 轉換程式庫。 驅動程式中的轉換會使用 Windows、Linux 或 macOS 轉換程式庫。 執行這些轉換時，這兩個程式庫可能會產生不同的結果。 如需詳細資訊，請參閱[終端使用者定義字元和專用區字元](/windows/desktop/Intl/end-user-defined-characters)。

- 如果用戶端編碼是 UTF-8，則驅動程式管理員不一定會正確地從 UTF-8 格式轉換為 UTF-16。 目前，字串中若有一或多個字元不是有效的 UTF-8 字元，即會發生資料損毀。 ASCII 字元會正確地對應。 在呼叫 ODBC API 的 SQLCHAR 版本 (例如 SQLDriverConnectA) 時，驅動程式管理員會嘗試這項轉換。 在呼叫 ODBC API 的 SQLWCHAR 版本 (例如 SQLDriverConnectW) 時，驅動程式管理員將不會嘗試這項轉換。  

- **SQLBindParameter** 的 *ColumnSize* 參數會參考 SQL 類型中的字元數，而 *BufferLength* 是應用程式緩衝區中的位元組數目。 不過，如果 SQL 資料類型是 `varchar(n)` 或 `char(n)`、應用程式繫結如 SQL_C_CHAR 或 SQL_C_VARCHAR 等參數，且用戶端的字元編碼為 UTF-8，則驅動程式可能會顯示「字串資料，右側截斷」的錯誤，即使 *ColumnSize* 的值與伺服器上的資料類型大小相符亦然。 因為字元編碼之間的轉換可能會變更資料長度，所以發生此錯誤。 例如，右單引號字元 (U+2019) 以 CP-1252 編碼時會成為單位元組 0x92，但以 UTF-8 編碼時會成為 3 個位元組的序列 0xe2 0x80 0x99。

例如，如果您的編碼為 UTF-8，並同時為 out 參數 **SQLBindParameter** 中的 *Columnsize* 和 *ColumnSize* 指定 1，然後嘗試擷取伺服器上儲存在 `char(1)` 資料行的前一個字元 (使用 CP-1252)，則驅動程式會嘗試將它轉換成 3 個位元組的 UTF-8 編碼方式，但無法將結果放入 1 個位元組的緩衝區內。 換個方向，它在執行用戶端與伺服器上不同字碼頁之間的轉換前，會先比較 **SQLBindParameter** 中的 *ColumnSize* 與 *BufferLength*。 由於 *ColumnSize* 1 小於 *BufferLength* 3 (舉例來說)，因此驅動程式會產生錯誤。 若要避免這個錯誤，請確認資料在轉換後的長度可放入指定的緩衝區或資料行內。 請注意，就 `varchar(n)` 類型而言，*ColumnSize* 不可大於 8000。

## <a name="see-also"></a>另請參閱  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[版本資訊](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

