---
description: SQLBindParameter (資料指標程式庫)
title: SQLBindParameter (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96fb4f3390b062a4b86f7a7b7f457c43c476c26c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466070"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLBindParameter** 函數。 如需 **SQLBindParameter**的一般資訊，請參閱 [SQLBindParameter 函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 只要系結資料行的 C 資料類型、資料行大小和小數位數保持不變，應用程式就可以呼叫 **SQLBindParameter** 來重新系結參數。  
  
 資料指標程式庫支援將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為使用系結位移。 不需要呼叫 (**SQLBindParameter** 就能進行此重新系結。 )   
  
 資料指標程式庫支援系結資料執行中參數。
