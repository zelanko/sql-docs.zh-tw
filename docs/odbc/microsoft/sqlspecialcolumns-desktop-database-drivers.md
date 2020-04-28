---
title: SQLSpecialColumns （桌面資料庫驅動程式） |Microsoft Docs
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
ms.openlocfilehash: 5f8cd4ed0912f9f1e71d64b32449b5d46f9ef1a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299388"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (桌面資料庫驅動程式)
系統會針對*fColType*中的 SQL_BEST_ROWID 旗標，傳回唯一索引（如果有的話）。 SQL_ROWVER 旗標不會傳回任何結果集。  
  
 所有資料列識別碼的範圍都是 SQL_SCOPE_CURROW。  
  
 *SzTableQualifier*或*szTableName*引數不支援模式比對。
