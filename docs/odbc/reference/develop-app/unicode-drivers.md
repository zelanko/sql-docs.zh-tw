---
title: Unicode 驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473036"
---
# <a name="unicode-drivers"></a>Unicode 驅動程式
Unicode 驅動程式或 ANSI 驅動程式，驅動程式是否應該是完全取決於資料來源的本質。 如果資料來源支援 Unicode 資料，則驅動程式應該是 Unicode 驅動程式。 如果資料來源只支援 ANSI 資料，則驅動程式應保留的 ANSI 驅動程式。  
  
 Unicode 驅動程式就必須匯出**SQLConnectW**被視為 Unicode 驅動程式透過驅動程式管理員。  
  
 Unicode 驅動程式必須接受 Unicode 函式 (尾碼*W*) 和儲存 Unicode 資料。 它也可以接受 ANSI 函式，但並不需要。 (驅動程式管理員不會通過 ANSI 函數呼叫，但*A*後置詞的驅動程式，但將它為 ansi 函式呼叫，而不需要後置詞和傳遞它的驅動程式。)  
  
 Unicode 驅動程式必須能夠在 Unicode 或 ANSI，傳回結果集，根據應用程式的繫結。 如果應用程式繫結至 SQL_C_CHAR，Unicode 驅動程式必須轉換 SQL_CHAR 的 SQL_WCHAR 資料。 驅動程式管理員會對應至 SQL_C_CHAR 的 SQL_C_WCHAR ANSI 驅動程式，但不會針對 Unicode 驅動程式沒有對應。  
  
> [!NOTE]  
>  判斷驅動程式類型，驅動程式管理員會呼叫**SQLSetConnectAttr** ，並在連接時將 SQL_ATTR_ANSI_APP 屬性。 如果應用程式使用的 ANSI Api，SQL_ATTR_ANSI_APP 將會設定為 SQL_AA_TRUE，而且如果它使用 Unicode，它會設定為 SQL_AA_FALSE 的值。 使驅動程式可以展現不同的行為取決於應用程式類型，則會使用這個屬性。 屬性無法設定應用程式直接與它不受支援**SQLGetConnectAttr**。 如果驅動程式展現相同的行為，ANSI 和 Unicode 應用程式，它應該傳回 SQL_ERROR，這個屬性。 如果驅動程式傳回 SQL_SUCCESS，驅動程式管理員會分隔 ANSI 和 Unicode 連線所使用的連接共用時。
