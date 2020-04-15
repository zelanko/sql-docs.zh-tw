---
title: SQLGet 函數(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307819"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 這個主題討論在游標庫中使用**SQLGet 函數函式**。 有關**SQLGet 函數**的一般資訊,請參閱[SQLGet 函數](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 呼叫**SQLGet 函數**時,游標庫返回它支援**SQL 擴充取得****、SQLFetchScroll、SQLSetPos**和**SQLSetScrollOptions,** 以及驅動程式支援的函數。 **SQLSetPos**
