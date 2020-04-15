---
title: 通用應用程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305549"
---
# <a name="generic-applications"></a>泛型應用程式
通用應用程式有時執行硬編碼任務,例如從資料庫檢索數據的電子錶格。 它們還可能執行各種使用者定義的任務,例如允許使用者輸入和執行 SQL 語句的通用查詢應用程式。 通用應用程式的共同點是,它們必須與各種不同的 DBMS 配合使用,並且開發人員事先不知道這些 DBMS 是什麼。  
  
 因此,通用應用程式需要高度可互通。 開發人員必須做出許多選擇,權衡功能的互操作性,並且必須編寫期望驅動程式支援各種功能的代碼。 雖然通用應用程式可能經過調整以使用流行的 DBMS,但它們很少包含特定於驅動程式或特定於 DBMS 的代碼。
