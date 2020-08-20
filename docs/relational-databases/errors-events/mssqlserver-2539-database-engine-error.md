---
description: MSSQLSERVER_2539
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7a3c22d94c510dcff4f1eb6d9c8a4b0af8b98486
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456259"
---
# <a name="mssqlserver_2539"></a>MSSQLSERVER_2539
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|2539|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|訊息文字|這個資料庫中的範圍總數目 = EXTENTS，使用的頁面 = USED_PAGES，保留的頁面 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>說明  
這項資訊是 DBCC CHECKALLOC 命令輸出的一部分， 也是指定資料庫中已配置範圍、已使用頁面和已保留頁面的摘要資訊。  
  
## <a name="user-action"></a>使用者動作  
None  
  
