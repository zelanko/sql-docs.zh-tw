---
title: 設定游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 805d8076c853513d86f9a3a92d9342d1224226c9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299798"
---
# <a name="setting-up-the-cursor"></a>設定資料指標
應用程式可以在執行創建結果集的語句之前指定游標類型。 它使用SQL_ATTR_CURSOR_TYPE語句屬性進行此用。 如果應用程式未顯式指定類型,將使用僅轉發游標。 要獲取混合游標,應用程式指定鍵集驅動的游標,但聲明鍵集大小小於結果集大小。  
  
 對於鍵集驅動和混合游標,應用程式還可以指定鍵集大小。 它使用SQL_ATTR_KEYSET_SIZE語句屬性進行此用。 如果鍵集大小設置為 0(預設值),則鍵集大小設置為結果集大小,並使用鍵集驅動的游標。 打開游標后,可以更改鍵集大小。  
  
 應用程式還可以設置行集大小;因此,應用程式還可以設置行集大小。有關詳細資訊,請參閱本節前面部分使用[塊游標](../../../odbc/reference/develop-app/using-block-cursors.md)。
