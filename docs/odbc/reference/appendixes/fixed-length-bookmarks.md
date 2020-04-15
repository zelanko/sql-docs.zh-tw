---
title: 固定長度書籤 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f90c5888a68506c056b2a56fce516080148528e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306979"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC *3. x*驅動程式應使用使用固定長度書籤的 ODBC *2.x*應用程式,則驅動程式必須支援以下內容:  
  
-   SQL_UB_ON作為SQL_USE_BOOKMARKS語句選項的值。 (SQL_UB_ON在 ODBC *3.x*中棄用)  
  
-   SQL_GET_BOOKMARK語句選項。
