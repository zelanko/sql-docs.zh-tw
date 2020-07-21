---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33302a6bccca3d83ef16172eaac7dcfc156ec3a8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551263"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|5231|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|訊息文字|物件識別碼 O_ID (物件 'NAME')：嘗試鎖定此物件進行檢查時發生死結。 已經略過這個物件，不會處理。|  
  
## <a name="explanation"></a>說明  
 DBCC 嘗試鎖定物件時發生死結，並已選擇 DBCC 做為死結犧牲者。 將不會處理此物件。  
  
## <a name="user-action"></a>使用者動作  
 None  
  
  
