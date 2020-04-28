---
title: 設定資料指標 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299798"
---
# <a name="setting-up-the-cursor"></a>設定資料指標
應用程式可以在執行建立結果集的語句之前，指定資料指標類型。 它會使用 SQL_ATTR_CURSOR_TYPE 語句屬性來執行此工作。 如果應用程式未明確指定類型，則會使用順向資料指標。 若要取得混合資料指標，應用程式會指定索引鍵集驅動資料指標，但是會宣告小於結果集大小的索引鍵集大小。  
  
 針對索引鍵集驅動和混合資料指標，應用程式也可以指定索引鍵集大小。 它會使用 SQL_ATTR_KEYSET_SIZE 語句屬性來執行此工作。 如果索引鍵集大小設定為0（這是預設值），則索引鍵集大小會設定為結果集大小，並使用索引鍵集驅動資料指標。 索引鍵集大小可以在資料指標開啟後變更。  
  
 應用程式也可以設定資料列集大小;如需詳細資訊，請參閱本節稍早的[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。
