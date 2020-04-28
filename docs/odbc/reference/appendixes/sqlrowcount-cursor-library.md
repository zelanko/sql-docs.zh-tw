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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9fe597f54ecb4bc82439251e2228ac5fdc4ea3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300588"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLRowCount**函數。 如需有關**SQLRowCount**的一般資訊，請參閱[SQLRowCount 函數](../../../odbc/reference/syntax/sqlrowcount-function.md)。  
  
 當應用程式使用與資料指標相關聯的語句來呼叫**SQLRowCount**時，資料指標程式庫會傳回它從驅動程式中取出的資料列數目。  
  
 當應用程式使用與定位 update 或 delete 語句相關聯的語句來呼叫**SQLRowCount**時，資料指標程式庫會傳回受語句影響的資料列數目。  
  
 當應用程式在**SELECT**語句之後呼叫**SQLRowCount**時，資料指標程式庫會傳回-1。
