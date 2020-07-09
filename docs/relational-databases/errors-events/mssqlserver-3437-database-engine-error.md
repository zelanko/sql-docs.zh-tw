---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e5b5d6fbed4c37d8e572b1c6e056f613e2152dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723481"
---
# <a name="mssqlserver_3437"></a>MSSQLSERVER_3437
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3437|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NODTC|  
|訊息文字|復原資料庫 '%.*ls' 時發生錯誤。 無法連接 Microsoft 分散式交易協調器 (MS DTC)，檢查交易 %S_XID 的完成狀態。 請修正 MS DTC，再次執行復原。|  
  
## <a name="explanation"></a>說明  
資料庫關閉時，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 的一個或多個分散式交易未完成。 此資料庫的復原失敗，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法連接 MS DTC 以完成或回復交易。  
  
## <a name="user-action"></a>使用者動作  
若要復原此資料庫，您必須先解決 MS DTC 的問題。 若要調查 MS DTC 的問題，請檢查 Windows 事件記錄檔。 如果無法解決 MS DTC 問題並復原資料庫，請還原資料庫備份。  
  
