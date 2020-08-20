---
description: MSSQLSERVER_5237
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5333d2f1cf5da680bff3f4b2dd15b6d52c677166
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470981"
---
# <a name="mssqlserver_5237"></a>MSSQLSERVER_5237
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|5237|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|訊息文字|物件 'NAME' (物件識別碼 O_ID) 的 DBCC 跨資料列集檢查失敗，因為發生內部查詢錯誤。|  
  
## <a name="explanation"></a>說明  
由於發生內部錯誤，導致 DBCC 無法執行查詢來檢查索引檢視表。  
  
## <a name="user-action"></a>使用者動作  
重新執行 DBCC 命令。  
  
