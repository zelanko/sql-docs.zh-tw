---
title: 安裝 SSMA for SAP ASE (SybaseToSQL) |Microsoft Docs
description: 使用這些文章來安裝、升級和卸載 SAP ASE 的 SQL Server 移轉小幫手，其中包括用戶端應用程式和延伸模組套件。
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fa1205a2511eb2c49c5be616caefad0ee0102105
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931602"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>安裝 SSMA for SAP ASE (SybaseToSQL) 
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP 彈性伺服器企業 (ASE) 的移轉小幫手 (SSMA) 包含一個用戶端應用程式，可讓您用來執行從 SAP ASE 遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 它也包含支援資料移轉的延伸模組套件，以及在您遷移的資料庫中使用 ASE 系統函數的功能。  
  
在您打算執行遷移步驟的電腦上安裝用戶端應用程式。 將延伸模組套件檔案安裝在執行的電腦上，並在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 其中主控已遷移的資料庫。  
  
## <a name="upgrading-ssma-for-sap-ase"></a>升級 SAP ASE 的 SSMA  
如果您想要升級至較新版本的 SSMA for SAP ASE，您必須先卸載用戶端和伺服器延伸模組套件。 然後安裝較新的版本。  
  
如果您從舊版的 SSMA for SAP ASE 開啟專案，SSMA 會詢問您是否要將專案轉換為較新的版本。 按一下 [**是]** 以在較新版本的 SSMA 中使用專案。  
  
## <a name="contents"></a>目錄  
  
|發行項|描述|  
|---------|---------------|  
|[安裝 SSMA for SAP ASE Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|提供安裝 SSMA for SAP ASE 用戶端的相關資訊和指示。|  
|[在 SQL Server &#40;SybaseToSQL 上安裝 SSMA 元件&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|提供在實例上安裝延伸模組套件的相關資訊和指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[移除 SSMA for SAP ASE Components &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|提供卸載用戶端程式和延伸模組套件的指示。|  
  
## <a name="see-also"></a>另請參閱  
[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
