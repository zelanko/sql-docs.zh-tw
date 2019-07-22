---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bd856be050972917f658d71f46a98393fe6ba7bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122764"
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|825|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|B_RETRYWORKED|  
|訊息文字|在位移 %#016I64x 之檔案 '%ls' 的讀取已成功，但之前已經失敗過 %d 次，錯誤為: %ls。 SQL Server 錯誤記錄檔和系統事件記錄檔中的訊息或許可以提供其他詳細資訊。 這個錯誤狀況可能會損及資料庫的完整性，所以必須更正。 請執行完整的資料庫一致性檢查 (DBCC CHECKDB)。 導致這個錯誤的原因有許多可能性; 如需詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
這個訊息表示讀取作業必須至少重新發出一次，也表示磁碟硬體發生嚴重問題。 這個訊息在目前並不表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有問題，但是磁碟問題若沒有解決，可能會導致資料遺失或資料庫損毀。 系統事件記錄檔可能包含相關事件，可協助診斷問題所在。 如需 I/O 錯誤的詳細資訊，請參閱[Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (第 2 章 Microsoft SQL Server I/O 基本概念)。  
  
## <a name="user-action"></a>使用者動作  
下列動作可以協助您找出並解決根本問題：  
  
-   檢閱錯誤記錄檔和此訊息中的變數文字，找出能夠解釋問題的線索。  
  
-   檢查您的磁碟系統。 問題可能與磁碟、磁碟控制卡、陣列卡，或磁碟驅動程式有關。  
  
-   連絡磁碟製造廠商，取得最新的公用程式，以檢查磁碟系統的狀態。  
  
-   連絡磁碟製造廠商，取得最新的驅動程式更新。  
  
