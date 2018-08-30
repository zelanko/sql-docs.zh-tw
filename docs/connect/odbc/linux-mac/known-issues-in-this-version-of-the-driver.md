---
title: 適用於 SQL Server 的已知問題，在這個版本的驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4a07cb8f8c5c3043ee307b7b7653846cc2d4e6e
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "42783878"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>此驅動程式版本的已知問題

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文包含 Microsoft ODBC Driver 13，13.1，17 for SQL Server 在 Linux 和 macOS 上的已知問題的清單。

其他問題會公佈於 [Microsoft ODBC 驅動程式團隊部落格](http://blogs.msdn.com/b/sqlnativeclient/)上。  

- Windows、Linux 和 macOS 可能會以不同的方式轉換來自專用區 (PUA) 或使用者定義字元 (EUDC) 的字元。 透過 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在伺服器上執行的轉換，會使用 Windows 轉換程式庫。 驅動程式中的轉換使用的 Windows、 Linux 或 macOS 轉換程式庫。 執行這些轉換時，這兩個程式庫可能會產生不同的結果。 如需詳細資訊，請參閱 [使用者定義字元和專用區字元](/windows/desktop/Intl/end-user-defined-characters)。

- 如果用戶端的編碼是 utf-8，驅動程式管理員不會不一定能夠正確轉換從 utf-8 為 utf-16。 目前，當字串中的一或多個字元並不是有效的 utf-8 字元時，就會發生資料損毀。 ASCII 字元都正確對應。 在呼叫 ODBC API 的 SQLCHAR 版本 (例如 SQLDriverConnectA) 時，驅動程式管理員會嘗試這項轉換。 在呼叫 ODBC API 的 SQLWCHAR 版本 (例如 SQLDriverConnectW) 時，驅動程式管理員將不會嘗試這項轉換。  

- *ColumnSize*的參數**SQLBindParameter**指的是 SQL 型別中的字元時*Columnsize*是在應用程式中的位元組數目緩衝區。 不過，如果 SQL 資料類型是 `varchar(n)` 或 `char(n)`、應用程式繫結如 SQL_C_CHAR 或 SQL_C_VARCHAR 等參數，且用戶端的字元編碼為 UTF-8，則驅動程式可能會顯示「字串資料，右側截斷」的錯誤，即使 *ColumnSize* 的值與伺服器上的資料類型大小相符亦然。 因為字元編碼之間的轉換可能會變更資料的長度，就會發生此錯誤。 例如，單引號字元 (U + 2019) 會編碼為 0x92，單一位元組的 CP-1252 但 utf-8 為 3 個位元組序列 0xe2 0x80 0x99。

例如，如果您的編碼為 utf-8，並同時指定 1 *Columnsize*並*ColumnSize*中**SQLBindParameter**的 out 參數，然後再嘗試擷取儲存在前一個字元`char(1)`資料行在伺服器上 （使用 CP-1252年），驅動程式會嘗試將它轉換成 3 個位元組 utf-8 編碼方式，但無法將結果納入 1 個位元組緩衝區。 另一個方向，它會比較*ColumnSize*具有*Columnsize*中**SQLBindParameter**才能執行不同的字碼頁之間的轉換入用戶端和伺服器。 由於 *ColumnSize* 1 小於 *BufferLength* 3 (舉例來說)，因此驅動程式會產生錯誤。 若要避免這個錯誤，請確認資料的長度之後轉換融入到指定的緩衝區或資料行。 請注意， *ColumnSize*不可大於 8000`varchar(n)`型別。

## <a name="see-also"></a>另請參閱  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)  

