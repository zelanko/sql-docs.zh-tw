---
title: "這個版本的驅動程式中的已知問題 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4202004a556479779d4884fc42d04ae540ed56d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="known-issues-in-this-version-of-the-driver"></a>此驅動程式版本的已知問題
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]本主題包含一份已知問題的 Microsoft ODBC Driver 13 for SQL Server on Linux 及 macOS。

其他問題會公佈於 [Microsoft ODBC 驅動程式團隊部落格](http://blogs.msdn.com/b/sqlnativeclient/)上。  

- Windows、 Linux 及 macOS 將字元轉換來自專用區 (PUA) 或使用者定義字元 (EUDC) 以不同的方式。 轉換內的伺服器上執行[!INCLUDE[tsql](../../../includes/tsql_md.md)]使用 Windows 轉換程式庫。 驅動程式中的轉換使用的 Windows、 Linux 或 macOS 轉換程式庫。 執行這些轉換時，每個程式庫可能會產生不同的結果。 如需詳細資訊，請參閱 [使用者定義字元和專用區字元](http://msdn.microsoft.com/library/dd317802.aspx)。

- 如果用戶端的編碼是 utf-8，驅動程式管理員不一定會正確轉換 utf-8 為 utf-16。 目前，1 時，會發生資料損毀，或字串中的多個字元不是有效的 utf-8 字元。 ASCII 字元會正確對應。 在呼叫 ODBC API 的 SQLCHAR 版本 (例如 SQLDriverConnectA) 時，驅動程式管理員會嘗試這項轉換。 在呼叫 ODBC API 的 SQLWCHAR 版本 (例如 SQLDriverConnectW) 時，驅動程式管理員將不會嘗試這項轉換。  

- *ColumnSize*參數**SQLBindParameter**指的是 SQL 型別中的字元時*Columnsize*是在應用程式中的位元組數緩衝區。 不過，如果 SQL 資料類型是`varchar(n)`或`char(n)`、 將參數繫結為 SQL_C_CHAR 或 SQL_C_VARCHAR，應用程式和用戶端的字元編碼為 utf-8，您可能會從驅動程式，即使收到 「 字串資料，右側截斷 」 的錯誤值*ColumnSize*配合伺服器上的資料類型的大小。 因為字元編碼之間的轉換可能會變更資料的長度，就會發生此錯誤。 例如，0x92 的單引號字元 (U + 2019) 以 cp-1252 成單一位元組 0x92，但為 3 個位元組序列 0xe2 utf-8 編碼 0x80 0x99。

例如，如果您的編碼是 utf-8，且您指定 1 兩個*Columnsize*和*ColumnSize*中**SQLBindParameter**的 out 參數，然後再嘗試擷取儲存在上述字元`char(1)`資料行在伺服器上 （使用 cp-1252），驅動程式會嘗試將它轉換成 3 個位元組 utf-8 編碼方式，但不能配合結果至 1 個位元組的緩衝區。 另一方向，它會比較*ColumnSize*與*Columnsize*中**SQLBindParameter**上執行不同的字碼頁之間的轉換之前用戶端和伺服器。 由於 *ColumnSize* 1 小於 *BufferLength* 3 (舉例來說)，因此驅動程式會產生錯誤。 若要避免這個錯誤，請確認資料的長度轉換符合指定的緩衝區或資料行之後。 請注意， *ColumnSize*不可大於 8000`varchar(n)`型別。

## <a name="see-also"></a>另請參閱  
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)  


