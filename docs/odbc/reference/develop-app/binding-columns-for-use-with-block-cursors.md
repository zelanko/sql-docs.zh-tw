---
description: 繫結資料行以搭配使用區塊資料指標
title: 系結資料行以搭配使用區塊資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a58e6359bd7b0ad5d44f75a3d844ef2e9872f2a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429440"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>繫結資料行以搭配使用區塊資料指標
因為區塊資料指標會傳回多個資料列，所以使用它們的應用程式必須將變數陣列系結至每個資料行，而不是單一變數。 這些陣列統稱為資料列 *集緩衝區*。 以下是兩種系結的樣式：  
  
-   將陣列系結至每個資料行。 這稱為資料 *行取向的* 系結，因為每個資料結構 (陣列) 包含單一資料行的資料。  
  
-   定義結構來保存整個資料列的資料，並系結這些結構的陣列。 這稱為資料 *列* 取向的系結，因為每個資料結構都包含單一資料列的資料。  
  
 當應用程式將單一變數系結至資料行時，它會呼叫 **SQLBindCol** 將陣列系結至資料行。 唯一的差別在於傳遞的位址是陣列位址，而不是單一變數位址。 應用程式會設定 SQL_BIND_BY_COLUMN 語句屬性，以指定其是否使用資料行取向或資料列取向的系結。 是否要使用資料行取向或資料列取向的系結，主要取決於應用程式喜好設定。 資料列取向的系結可能更緊密地對應到應用程式的資料版面配置，在這種情況下，它會提供更好的效能。  
  
 此章節包含下列主題。  
  
-   [資料行取向的系結](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [資料列取向的系結](../../../odbc/reference/develop-app/row-wise-binding.md)
