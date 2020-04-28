---
title: 安裝 SSMA for SAP ASE （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 91a4dfcf8add3900c51e33a6e40fa874ce9f9798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028969"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>安裝 SSMA for SAP ASE （SybaseToSQL）
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]適用于 SAP 調適型伺服器 Enterprise （ASE）的移轉小幫手（SSMA）是由您用來執行從 SAP ASE 遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 的用戶端應用程式所組成。 它也包含支援資料移轉的延伸模組套件，以及在您遷移的資料庫中使用 ASE 系統函數的功能。  
  
在您打算執行遷移步驟的電腦上安裝用戶端應用程式。 將延伸模組套件檔案安裝在執行的電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上，並在其中主控已遷移的資料庫。  
  
## <a name="upgrading-ssma-for-sap-ase"></a>升級 SAP ASE 的 SSMA  
如果您想要升級至較新版本的 SSMA for SAP ASE，您必須先卸載用戶端和伺服器延伸模組套件。 然後安裝較新的版本。  
  
如果您從舊版的 SSMA for SAP ASE 開啟專案，SSMA 會詢問您是否要將專案轉換為較新的版本。 按一下 [**是]** 以在較新版本的 SSMA 中使用專案。  
  
## <a name="contents"></a>內容  
  
|發行項|描述|  
|---------|---------------|  
|[安裝 SSMA for SAP ASE Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|提供安裝 SSMA for SAP ASE 用戶端的相關資訊和指示。|  
|[在 SQL Server &#40;SybaseToSQL 上安裝 SSMA 元件&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|提供在實例上安裝延伸模組套件的相關資訊和指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|[移除 SSMA for SAP ASE Components &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|提供卸載用戶端程式和延伸模組套件的指示。|  
  
## <a name="see-also"></a>另請參閱  
[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
