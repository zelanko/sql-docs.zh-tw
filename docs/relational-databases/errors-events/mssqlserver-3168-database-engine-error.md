---
title: MSSQLSERVER_3168 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3168 (Database Engine error)
ms.assetid: 991111d9-1eb3-43e9-9333-a75a775c3200
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4812a171f8693294d7e9d9665e744b21a6284c55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723698"
---
# <a name="mssqlserver_3168"></a>MSSQLSERVER_3168
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|3168|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_SYSTEMWRONGVER|  
|訊息文字|裝置 %ls 上的系統資料庫備份無法還原，因為它是由不同於這個伺服器版本 (%ls) 的版本 (%ls) 所建立。|  
  
## <a name="explanation"></a>說明  
在不同於原先執行備份之組建的伺服器組建上，您無法還原系統資料庫 (**master**、**model** 或 **msdb**) 的備份。  
  
> [!NOTE]  
> 安裝 Service Pack 或 Hotfix 組建會變更伺服器的組建編號，而且伺服器的組建一定是累加的。  
  
### <a name="possible-causes"></a>可能的原因  
在不同的伺服器組建之間，系統資料庫的資料庫結構描述可能已有所變更。 為了確保這項結構描述變更不會造成任何不一致性，RESTORE 陳述式會將備份檔案的伺服器組建編號，與您嘗試還原備份所在之伺服器的組建編號進行比較。 如果這兩個組建不同，陳述式將發出 3168 錯誤訊息，並且還原作業會異常終止。  
  
下列是可能會發生這個問題的案例：  
  
-   使用者嘗試在伺服器 A 上還原取自伺服器 B 的系統資料庫備份。伺服器 A 和伺服器 B 是不同的伺服器組建。 例如，伺服器 A 可能是原始發行版本組建，而伺服器 B 是 Service Pack 1 (SP1) 組建。  
  
-   使用者嘗試還原取自相同伺服器的系統資料庫備份， 但在進行備份時，伺服器執行的是不同的組建。 也就是說，自從執行備份之後，伺服器已升級。  
  
## <a name="user-action"></a>使用者動作  
這種情況下的還原程序相當複雜，如非必要，請勿使用。 如需詳細資訊，請參閱[您無法將系統資料庫備份還原至不同的 SQL Server 組建](https://support.microsoft.com/kb/264474)。  
  
## <a name="see-also"></a>另請參閱  
[系統資料庫的備份與還原 &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
