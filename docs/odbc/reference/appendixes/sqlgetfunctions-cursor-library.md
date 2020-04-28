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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f993a08aae1656b8d373911299e75852de855419
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307819"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLGetFunctions**函數。 如需有關**SQLGetFunctions**的一般資訊，請參閱[SQLGetFunctions 函數](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 當您呼叫**SQLGetFunctions**時，資料指標程式庫會傳回它支援**SQLExtendedFetch**、 **SQLFetchScroll**、 **SQLSetPos**和**SQLSetScrollOptions**，以及驅動程式所支援的函數。
