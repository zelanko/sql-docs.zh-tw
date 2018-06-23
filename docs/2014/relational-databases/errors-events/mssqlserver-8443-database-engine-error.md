---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d6e7ccc935f09bf69e848ead0a906365eeb5fe2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136146"
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|8443|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SB_DIALOG_WO_CONV_GROUP|  
|訊息文字|具有識別碼 '%.*ls' 和起始端 %d 的交談參考了遺漏的交談群組 '%.\*ls'。 請執行 DBCC CHECKDB 來分析和修復資料庫。|  
  
## <a name="explanation"></a>說明  
 中繼資料層針對交談群組傳回 NULL。 資料庫在某些方面發生損毀。 其中一個可能的損毀來源是磁碟錯誤。  
  
## <a name="user-action"></a>使用者動作  
 以修復模式執行 DBCC CHECKDB，使資料庫回復到一致的狀態。 此命令可能會在必要時刪除訊息，以還原一致性。 請查閲系統錯誤記錄檔，確定這項錯誤是否由於其他系統錯誤所造成。  
  
  