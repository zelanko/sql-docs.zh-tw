---
title: Unicode 驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284350"
---
# <a name="unicode-drivers"></a>Unicode 驅動程式
驅動程式是 Unicode 驅動程式還是 ANSI 驅動程式完全取決於資料源的性質。 如果數據源支援 Unicode 數據,則驅動程式應為 Unicode 驅動程式。 如果資料來源僅支援 ANSI 資料,則驅動程式應仍為 ANSI 驅動程式。  
  
 Unicode 驅動程式必須匯出**SQLConnectW**才能被驅動程式管理員識別為 Unicode 驅動程式。  
  
 Unicode 驅動程式必須接受 Unicode 函數(後綴為*W)* 並存儲 Unicode 資料。 它也可以接受 ANSI 函數,但不是必需的。 (驅動程式管理員不會將帶有*A*後綴的 ANSI 函數呼叫傳遞給驅動程式,而是將其轉換為沒有後綴的 ANSI 函數調用,然後將其傳遞給驅動程式。  
  
 Unicode 驅動程式必須能夠返回 Unicode 或 ANSI 中的結果集,具體取決於應用程式的綁定。 如果應用程式綁定到SQL_C_CHAR,Unicode 驅動程式必須將SQL_WCHAR數據轉換為SQL_CHAR。 驅動程式管理員將SQL_C_WCHAR映射到 ANSI 驅動程式SQL_C_CHAR,但不映射 Unicode 驅動程式。  
  
> [!NOTE]  
>  確定驅動程式類型時,驅動程式管理員將調用**SQLSetConnectAttr**並在連接時設定SQL_ATTR_ANSI_APP屬性。 如果應用程式使用 ANSI API,SQL_ATTR_ANSI_APP將設定為SQL_AA_TRUE,如果應用程式使用 Unicode,則它將設置為SQL_AA_FALSE的值。 使用此屬性,以便驅動程式可以基於應用程式類型顯示不同的行為。 該屬性不能由應用程式直接設置,並且**SQLGetConnectAttr**不支援該屬性。 如果驅動程式對 ANSI 和 Unicode 應用程式都表現出相同的行為,則應傳回此屬性SQL_ERROR。 如果驅動程式返回SQL_SUCCESS,則驅動程式管理器將在使用連接池時分離 ANSI 和 Unicode 連接。
