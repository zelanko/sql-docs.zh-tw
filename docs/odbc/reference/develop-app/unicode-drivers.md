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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284350"
---
# <a name="unicode-drivers"></a>Unicode 驅動程式
驅動程式是否應為 Unicode 驅動程式或 ANSI 驅動程式，完全取決於資料來源的本質。 如果資料來源支援 Unicode 資料，驅動程式應該是 Unicode 驅動程式。 如果資料來源僅支援 ANSI 資料，驅動程式應該會保留 ANSI 驅動程式。  
  
 Unicode 驅動程式必須匯出**SQLConnectW** ，才能由驅動程式管理員識別為 Unicode 驅動程式。  
  
 Unicode 驅動程式必須接受 Unicode 函式（尾碼為*W*）並儲存 unicode 資料。 它也可以接受 ANSI 函式，但不需要這麼做。 （驅動程式管理員不會將具有後置*詞的 ansi*函數呼叫傳遞給驅動程式，但會將它轉換成不含尾碼的 ansi 函式呼叫，然後將它傳遞給驅動程式）。  
  
 Unicode 驅動程式必須能夠以 Unicode 或 ANSI 傳回結果集，端視應用程式的系結而定。 如果應用程式系結至 SQL_C_CHAR，Unicode 驅動程式必須將 SQL_WCHAR 資料轉換成 SQL_CHAR。 驅動程式管理員會將 SQL_C_WCHAR 對應到 ANSI 驅動程式 SQL_C_CHAR，但不會對應 Unicode 驅動程式。  
  
> [!NOTE]  
>  在決定驅動程式類型時，驅動程式管理員會呼叫**SQLSetConnectAttr** ，並在連接時設定 SQL_ATTR_ANSI_APP 屬性。 如果應用程式使用 ANSI Api，SQL_ATTR_ANSI_APP 將會設定為 SQL_AA_TRUE，而如果使用 Unicode，則會設定為 SQL_AA_FALSE 的值。 此屬性是用來讓驅動程式根據應用程式類型來展現不同的行為。 應用程式無法直接設定屬性，而且**SQLGetConnectAttr**不支援。 如果驅動程式在 ANSI 和 Unicode 應用程式中都有相同的行為，它應該會傳回這個屬性的 SQL_ERROR。 如果驅動程式傳回 SQL_SUCCESS，則使用連接共用時，驅動程式管理員將會分隔 ANSI 和 Unicode 連接。
