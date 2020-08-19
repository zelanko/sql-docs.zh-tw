---
description: SQLSpecialColumns (桌面資料庫驅動程式)
title: SQLSpecialColumns (桌面資料庫驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3f023c4f82c5a2f9af7af2e34cc697ffdb34206
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421612"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (桌面資料庫驅動程式)
如果 *fColType*中的 SQL_BEST_ROWID 旗標有) ，則會傳回唯一索引 (。 SQL_ROWVER 旗標將不會傳回任何結果集。  
  
 所有資料列識別碼都有 SQL_SCOPE_CURROW 範圍。  
  
 *SzTableQualifier*或*szTableName*引數不支援模式比對。
