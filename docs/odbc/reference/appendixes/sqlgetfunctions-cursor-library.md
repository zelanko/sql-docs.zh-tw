---
title: SQLGetFunctions （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1123a6497207f40bd210edf35b9b4477bc9c7b6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188725"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetFunctions**資料指標程式庫中的函式。 如需一般資訊**SQLGetFunctions**，請參閱[SQLGetFunctions 函數](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 當您呼叫**SQLGetFunctions**，資料指標程式庫會傳回它支援**SQLExtendedFetch**， **SQLFetchScroll**， **SQLSetPos**，並**SQLSetScrollOptions**，除了驅動程式支援的函式。
