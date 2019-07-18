---
title: SQLSetEnvAttr 和資料指標程式庫 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1608415ae74bcaafd89f4afe01393cfb700379
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125562"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和資料指標程式庫
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLSetEnvAttr**函式與資料指標程式庫。 如需一般資訊**SQLSetEnvAttr**，請參閱[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 資料指標程式庫不會受到 SQL_ATTR_ODBC_VERSION 環境的屬性，不論應用程式版本或驅動程式版本的設定。
