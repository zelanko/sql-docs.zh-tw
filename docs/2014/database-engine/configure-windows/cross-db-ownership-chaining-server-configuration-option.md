---
title: cross db ownership chaining 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5630579e787a3bfcb5d64ee3bcf0ec5bee368611
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782391"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>跨資料庫擁有權鏈結伺服器組態選項
  使用 [跨資料庫擁有權鏈結]**** 選項，可為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體設定跨資料庫擁有權鏈結。  
  
 此伺服器選項允許您在資料庫層級控制跨資料庫擁有權鏈結，或允許所有資料庫的跨資料庫擁有權鏈結：  
  
-   當執行個體的 [跨資料庫擁有權鏈結]**** 設定為關閉 (0) 時，所有資料庫的跨資料庫擁有權鏈結都會停用。  
  
-   當執行個體的 [跨資料庫擁有權鏈結]**** 設定為開啟 (1) 時，所有資料庫的跨資料庫擁有權鏈結都會開啟。  
  
-   您可以使用 ALTER DATABASE 陳述式的 SET 子句，來設定個別資料庫的跨資料庫擁有權鏈結。 若您要建立新的資料庫，您可以使用 CREATE DATABASE 陳述式，來為新的資料庫設定跨資料庫擁有權鏈結選項。  
  
     除非 ** 執行個體所裝載的資料庫都必須參與跨資料庫擁有權鏈結，而且您了解此設定的安全性含意，否則不建議將 [跨資料庫擁有權鏈結]**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為 1。  
  
## <a name="controlling-cross-database-ownership-chaining"></a>控制跨資料庫擁有權鏈結  
 在開啟或關閉跨資料庫擁有權鏈結之前，請考量下列事項：  
  
-   您必須是 **系統管理員** 固定伺服器角色的成員，才能開啟或關閉跨資料庫擁有權鏈結。  
  
-   在產品伺服器上關閉跨資料庫擁有權鏈結，請完整測試所有的應用程式 (包含協力廠商應用程式)，才能確定變更不會影響應用程式功能。  
  
-   若您以 **sp_configure** 來指定 RECONFIGURE，當伺服器執行時，您可以變更 [跨資料庫擁有權鏈結]**** 選項。  
  
-   若您有資料庫需要跨資料庫擁有權鏈結，建議您使用 **sp_configure** 來關閉執行個體的 [跨資料庫擁有權鏈結]**** 選項，再使用 ALTER DATABASE 陳述式來為有需要的個別資料庫，開啟跨資料庫擁有權鏈結。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [建立資料庫 &#40;SQL Server Transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
