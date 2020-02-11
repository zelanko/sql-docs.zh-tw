---
title: SQLNativeSql （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c42efbd87296cf7157d75d1848e4655247818
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125706"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLNativeSql**函數。 如需有關**SQLNativeSql**的一般資訊，請參閱[SQLNativeSql 函數](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驅動程式支援此函式，則資料指標程式庫會呼叫驅動程式中的**SQLNativeSql** ，並將它傳遞至 SQL 語句。 若為定點更新、定位 delete，然後**選取 update**語句，則資料指標程式庫會先修改語句，再將它傳遞給驅動程式。  
  
> [!NOTE]  
>  如果在**SQLNativeSql**的*InStatementText*引數中傳遞的定點更新或 delete 語句中的資料指標名稱無效，則資料指標程式庫會錯誤地傳回 SQLSTATE 34000 （不正確資料指標名稱）。 **SQLNativeSql**不是用來傳回語法錯誤，只會在語句準備或執行時傳回。
