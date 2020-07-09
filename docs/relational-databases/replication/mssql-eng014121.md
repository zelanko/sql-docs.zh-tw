---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 53ca3338b2b3f603d613712ea5021efb7d132aaa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85721889"
---
# <a name="mssql_eng014121"></a>MSSQL_ENG014121
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14121|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法卸除散發者 '%s'。 這個散發者有相關聯的散發資料庫。|  
  
## <a name="explanation"></a>說明  
 設定為「散發者」的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體不能從「散發者」的角色中移除，因為散發資料庫與此執行個體關聯。 若您嘗試卸除與一個或多個發行者相關聯的散發資料庫，就會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 若要尋找已與此「散發者」建立關聯之任何「發行者」及散發資料庫的名稱，請從「散發者」的所有資料庫中執行 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)。  
  
 針對已與此「散發者」建立關聯的所有散發資料庫，執行 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)。 在移除了所有散發資料庫關聯後，您可以停用散發。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
