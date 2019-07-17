---
title: SQLRowCount （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be902866cfcf98a10af2c3741926de8b7541bb79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125602"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLRowCount**資料指標程式庫中的函式。 如需一般資訊**SQLRowCount**，請參閱[SQLRowCount 函式](../../../odbc/reference/syntax/sqlrowcount-function.md)。  
  
 當應用程式呼叫**SQLRowCount**資料指標程式庫會傳回資料指標相關聯的陳述式，它已從驅動程式擷取的資料列數目。  
  
 當應用程式呼叫**SQLRowCount**定位的 update 或 delete 陳述式相關聯的陳述式，資料指標程式庫會傳回的陳述式所影響的資料列數目。  
  
 當應用程式呼叫**SQLRowCount**之後**選取**陳述式中，資料指標程式庫會傳回-1。
