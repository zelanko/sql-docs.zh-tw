---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6be551a13382279401648b1579b542a71142dd23
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717060"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
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
  
