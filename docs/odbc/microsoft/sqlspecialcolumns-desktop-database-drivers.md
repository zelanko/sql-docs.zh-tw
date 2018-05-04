---
title: SQLSpecialColumns （桌面資料庫驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2d2bfda1bb8732e3036c3803628bbe8247f9e76
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns （桌面資料庫驅動程式）
唯一的索引就會傳回 （如果有的話） 中的 SQL_BEST_ROWID 旗標*fColType*。 SQL_ROWVER 旗標，就會不傳回任何結果集。  
  
 所有資料列識別碼具有針對 SQL_SCOPE_CURROW 領域。  
  
 模式比對不支援針對*szTableQualifier*或*szTableName*引數。
