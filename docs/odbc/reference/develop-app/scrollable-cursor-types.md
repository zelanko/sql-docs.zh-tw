---
description: 可捲動的資料指標類型
title: 可滾動的資料指標類型 |Microsoft Docs
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
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c27ccd54bfe0ba099d78c002fce4c901e4bf8c1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476510"
---
# <a name="scrollable-cursor-types"></a>可捲動的資料指標類型
這四種可滾動的資料指標類型為靜態、動態、索引鍵集驅動和混合。 靜態資料指標會偵測幾個或沒有任何變更，但要執行的成本相對較低。 動態資料指標會偵測到所有變更，但要執行的成本很高。 索引鍵集驅動和混合的資料指標位於兩者之間，偵測大部分的變更，但成本低於動態資料指標。  
  
 下列詞彙是用來定義每種可滾動資料指標類型的特性：  
  
-   **擁有更新、刪除和插入。** 透過呼叫 **SQLBulkOperations** 或 **SQLSetPos** ，或使用定位的 update 或 delete 語句，透過資料指標進行更新、刪除和插入。  
  
-   **其他更新、刪除和插入。** 不是由資料指標所進行的更新、刪除和插入，包括其他作業在相同交易中所做的更新、透過其他交易進行的作業，以及其他應用程式所做的更新。  
  
-   **會員。** 結果集中的資料列集。  
  
-   **以。** 資料指標傳回資料列的順序。  
  
-   **值。** 結果集中每個資料列的值。  
  
 如需有關如何更新、刪除和插入資料的詳細資訊，請參閱 [更新資料總覽](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 靜態資料指標](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動態資料指標](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [索引鍵集導向的資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合資料指標](../../../odbc/reference/develop-app/mixed-cursors.md)
