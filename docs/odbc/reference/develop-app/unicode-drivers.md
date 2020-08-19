---
description: Unicode 驅動程式
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
ms.openlocfilehash: 1acdb0c630fe5f4b1b22f51015e7ee94e7d8a56a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424480"
---
# <a name="unicode-drivers"></a>Unicode 驅動程式
驅動程式是否應該是 Unicode 驅動程式或 ANSI 驅動程式，完全取決於資料來源的本質。 如果資料來源支援 Unicode 資料，驅動程式應該是 Unicode 驅動程式。 如果資料來源只支援 ANSI 資料，驅動程式應該仍為 ANSI 驅動程式。  
  
 Unicode 驅動程式必須匯出 **SQLConnectW** ，驅動程式管理員才能將其辨識為 Unicode 驅動程式。  
  
 Unicode 驅動程式必須接受 (尾碼為 *W*) 的 unicode 函數，並儲存 unicode 資料。 它也可以接受 ANSI 函數，但不需要。  (驅動程式管理員不 *會將具有尾碼的* ansi 函式呼叫傳遞至驅動程式，但是會將它轉換成不含尾碼的 ansi 函式呼叫，然後將其傳遞至驅動程式。 )   
  
 Unicode 驅動程式必須能夠根據應用程式的系結，傳回 Unicode 或 ANSI 的結果集。 如果應用程式系結至 SQL_C_CHAR，則 Unicode 驅動程式必須將 SQL_WCHAR 資料轉換成 SQL_CHAR。 驅動程式管理員會將 SQL_C_WCHAR 對應至 ANSI 驅動程式 SQL_C_CHAR，但不會對應 Unicode 驅動程式。  
  
> [!NOTE]  
>  判斷驅動程式類型時，驅動程式管理員會呼叫 **SQLSetConnectAttr** ，並在連接時設定 SQL_ATTR_ANSI_APP 屬性。 如果應用程式使用 ANSI Api，SQL_ATTR_ANSI_APP 將設定為 SQL_AA_TRUE，而且如果使用 Unicode，則會將它設定為 [SQL_AA_FALSE] 的值。 使用這個屬性時，驅動程式可能會根據應用程式類型展現不同的行為。 應用程式無法直接設定屬性， **SQLGetConnectAttr**不支援此屬性。 如果針對 ANSI 和 Unicode 應用程式，驅動程式的行為相同，則應該傳回此屬性 SQL_ERROR。 如果驅動程式傳回 SQL_SUCCESS，則使用連接共用時，驅動程式管理員會分隔 ANSI 和 Unicode 連接。
