---
title: MSSQLSERVER_823 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7ece8314c37546b29ab27451a75d2a1866aebc30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913220"
---
# <a name="mssqlserver823"></a>MSSQLSERVER_823
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|823|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|B_HARDERR|  
|訊息文字|作業系統將錯誤 %ls 傳回給 SQL Server，期間：%S_MSG 在 %#016I64x 位移，檔案：'%ls'。 SQL Server 錯誤記錄檔和系統事件記錄檔中的訊息或許可以提供其他詳細資訊。 這是嚴重的系統層級錯誤狀況，且可能會損及資料庫的完整性，所以必須立即更正。 請執行完整的資料庫一致性檢查 (DBCC CHECKDB)。 導致這個錯誤的原因有許多可能性; 如需詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
 Windows 讀取或寫入要求失敗。 Windows 傳回的錯誤碼和對應的文字都已插入訊息中。 在讀取案例中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經重試讀取要求四次。 這個錯誤通常是硬體錯誤所造成的結果，但也可能是裝置驅動程式所引起的。 如需錯誤 823 的詳細資訊，請參閱 [https://support.microsoft.com/kb/828339](https://support.microsoft.com/kb/828339)。 如需 I/O 錯誤的詳細資訊，請參閱[Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (第 2 章 Microsoft SQL Server I/O 基本概念)。  
  
## <a name="user-action"></a>使用者動作  
 查看系統事件記錄檔中的其他資訊， 並連絡硬體製造商或 Microsoft 客戶服務及支援中心，確定其原因與更正動作。 更正硬體錯誤之後，請還原所有資料庫並執行 DBCC CHECKDB。  
  
  
