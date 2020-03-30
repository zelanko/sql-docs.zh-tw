---
title: MSSQLSERVER_2527 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc2b1094a4ea7f8f6c2d2d60c804260286c5f237
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68085987"
---
# <a name="mssqlserver_2527"></a>MSSQLSERVER_2527
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2527|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|訊息文字|無法處理資料表 O_NAME 的索引 I_NAME，因為檔案群組 F_NAME 已離線。|  
  
## <a name="explanation"></a>說明  
這項參考用訊息指出由於儲存索引資料的其中一個檔案群組已離線，因此無法檢查索引。 檔案群組中的檔案狀態將決定整個檔案群組的可用性。 若要使某個檔案群組為可用的，則在檔案群組中的所有檔案必須都在線上。 如果沒有其他問題，將會檢查相同物件的所有其他索引。  
  
## <a name="user-action"></a>使用者動作  
若要針對指定的檔案群組檢查檔案的狀態，請查詢 **sys.database_files** 或 **sys.master_files** 目錄檢視。  
  
從備份還原離線檔案。  
  
## <a name="see-also"></a>另請參閱  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
