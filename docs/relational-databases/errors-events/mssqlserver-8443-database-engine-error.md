---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d4a7ee12d9462c8772c0e005c76d5dd12445b99a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727511"
---
# <a name="mssqlserver_8443"></a>MSSQLSERVER_8443
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|8443|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SB_DIALOG_WO_CONV_GROUP|  
|訊息文字|具有識別碼 '%.*ls' 和起始端 %d 的交談參考了遺漏的交談群組 '%.\*ls'。 請執行 DBCC CHECKDB 來分析和修復資料庫。|  
  
## <a name="explanation"></a>說明  
中繼資料層針對交談群組傳回 NULL。 資料庫在某些方面發生損毀。 其中一個可能的損毀來源是磁碟錯誤。  
  
## <a name="user-action"></a>使用者動作  
以修復模式執行 DBCC CHECKDB，使資料庫回復到一致的狀態。 此命令可能會在必要時刪除訊息，以還原一致性。 請查閲系統錯誤記錄檔，確定這項錯誤是否由於其他系統錯誤所造成。  
  
