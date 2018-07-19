---
title: SQLGetFunctions （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57cfb7dba02ab91a918d898a0ad14764599340f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906663"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetFunctions**資料指標程式庫中的函式。 如需一般資訊**SQLGetFunctions**，請參閱[SQLGetFunctions 函數](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 當您呼叫**SQLGetFunctions**，資料指標程式庫會傳回它支援**SQLExtendedFetch**， **SQLFetchScroll**， **SQLSetPos**，和**SQLSetScrollOptions**，除了驅動程式支援的函式。
