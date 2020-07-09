---
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16a79a049ea1b1beaba79ec94c980c73e9614a00
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780306"
---
# <a name="mssqlserver_2538"></a>MSSQLSERVER_2538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|2538|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|訊息文字|檔案 FILE。 範圍數目 = EXTENTS，使用的頁面 = USED_PAGES，保留的頁面 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>說明  
這項資訊是 DBCC CHECKALLOC 命令輸出的一部分， 也是指定資料庫中已配置範圍、已使用頁面和已保留頁面的個別檔案摘要資訊。  
  
## <a name="user-action"></a>使用者動作  
None  
  
