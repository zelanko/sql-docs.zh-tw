---
title: 檢視 SQL Server 錯誤記錄檔 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 38d99822b2d77e25259c793d350e4d329d4c0af7
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582223"
---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>檢視 SQL Server 錯誤記錄檔 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔包含使用者定義事件和特定系統事件，以用於進行疑難排解。 

## <a name="view-the-logs"></a>檢視記錄檔

1. 在 SQL Server Management Studio 中，選取 [物件總管]  。 若要開啟 [物件總管]  ，請選取 F8。 或者，在上層功能表上，選取 [檢視]  ，然後選取 [物件總管]  ：
    
    ![物件總管](../../relational-databases/performance/media/object-explorer.png) 

2. 在 [物件總管]  中，連線到 SQL Server 的執行個體，然後展開該執行個體。
  
3. 尋找並展開 [管理]  區段 (假設您有權限可以看到它)。

4. 以滑鼠右鍵按一下 [SQL Server 記錄檔]  ，選取 [檢視]  ，然後選擇 [SQL Server 記錄檔]  。

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5. [記錄檔檢視器]  會隨即顯示 (可能需要一點時間)，內含可供您檢視的記錄檔清單。

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

  ## <a name="see-also"></a>另請參閱
  如需詳細資訊，請參閱 [MSSQLTips.com 的](https://www.mssqltips.com/)實用文章：[Identify location of the SQL Server Error Log file](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/) (識別 SQL Server 錯誤記錄檔的位置)。

