---
description: CREATE INDEX 陳述式
title: CREATE INDEX 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483631"
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 語句的語法為：  
  
 CREATE [UNIQUE] INDEX *index-* *資料表* 名稱 (資料 *行識別碼* [ASC] [DESC] [，資料 *行識別碼* [asc] [desc] ...]) \<*index option list*>  
  
 其中 \<*index option list*> 可以是：主要 &#124; 不允許 null &#124; 忽略 null  
  
 只有 Microsoft Access 驅動程式會使用不允許的 Null 和 IGNORE Null 索引選項。 DBASE 和 Paradox 驅動程式會接受語法，但忽略任一選項的存在。  
  
 使用 Paradox 驅動程式時，CREATE INDEX 語句會建立 Paradox 的主要金鑰檔和次要檔案。  
  
 Microsoft Excel 或文字驅動程式不支援此語句。
