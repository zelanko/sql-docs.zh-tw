---
title: 服務主要金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 6ea074466c8075b7fb1746b7d3eb8741425b44c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011322"
---
# <a name="service-master-key"></a>服務主要金鑰
  「服務主要金鑰」是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 加密階層的根。 第一次需要利用這種金鑰來加密其他金鑰時，便會自動產生服務主要金鑰。 依預設，服務主要金鑰是以 Windows 資料保護 API 以及本機電腦金鑰加密。 服務主要金鑰只能由建立此金鑰的 Windows 服務帳戶來開啟，或是由可存取服務帳戶名稱及其密碼的主體來開啟。  
  
 重新產生或還原服務主要金鑰包括解密與重新加密完整的加密階層。 除非該金鑰已經洩密，才應該在資源需求低的時段，排程進行此項會耗用大量資源的作業。  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 是使用 AES 加密演算法來保護服務主要金鑰 (SMK) 及資料庫主要金鑰 (DMK)。 與舊版中使用的 3DES 相比，AES 是一種較新的加密演算法。 將 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 執行個體升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 之後，應該會重新產生 SMK 和 DMK，以將主要金鑰升級至 AES。 如需重新產生 SMK 的詳細資訊，請參閱 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql) 和 [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql)。  
  
## <a name="best-practice"></a>最佳作法  
 備份服務主要金鑰，然後在一個安全且位於異地的位置存放此金鑰備份。  
  
## <a name="related-tasks"></a>相關工作  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [加密階層](encryption-hierarchy.md)  
  
  
