---
description: SQLSetEnvAttr 和資料指標程式庫
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97751c4735ed7357b87a3b50df5f116f7bb38c7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476930"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和資料指標程式庫
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何搭配使用 **SQLSetEnvAttr** 函式和資料指標程式庫。 如需 **SQLSetEnvAttr**的一般資訊，請參閱 [SQLSetEnvAttr 函數](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 無論應用程式版本或驅動程式版本為何，資料指標程式庫都不會受到 SQL_ATTR_ODBC_VERSION 環境屬性的設定影響。
