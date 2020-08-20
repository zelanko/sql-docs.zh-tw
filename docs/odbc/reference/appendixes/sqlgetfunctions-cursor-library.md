---
description: SQLGetFunctions (資料指標程式庫)
title: SQLGetFunctions (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: ac307fbc1dcd2b10777ebe2e92f48f053ffcbd6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499971"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLGetFunctions** 函數。 如需 **SQLGetFunctions**的一般資訊，請參閱 [SQLGetFunctions 函數](../../../odbc/reference/syntax/sqlgetfunctions-function.md)。  
  
 當您呼叫 **SQLGetFunctions**時，資料指標程式庫會傳回它除了驅動程式支援的函式之外，還支援 **SQLExtendedFetch**、 **SQLFetchScroll**、 **SQLSetPos**和 **SQLSetScrollOptions**。
