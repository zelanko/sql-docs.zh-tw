---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eadb07e1f7add72d181546a3c1a74c9bbf6ca406
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85693962"
---
# <a name="mssqlserver_7916"></a>MSSQLSERVER_7916
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|7916|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_REPAIR_RECORD|  
|訊息文字|修復:已刪除頁面 P_ID，位置 S_ID 上的物件識別碼 O_ID，索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE) 之記錄。 將會重建索引。|  
  
## <a name="explanation"></a>說明  
這是來自 REPAIR 的參考用訊息，指出已經從頁面中刪除指定的記錄。  
  
## <a name="user-action"></a>使用者動作  
None  
  
