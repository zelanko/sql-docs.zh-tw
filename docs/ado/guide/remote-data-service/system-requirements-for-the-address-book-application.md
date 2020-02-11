---
title: 通訊錄應用程式的系統需求 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2450cc97229a6629d4c2895f3960e3033d129789
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922030"
---
# <a name="system-requirements-for-the-address-book-application"></a>通訊錄應用程式的系統需求
若要設定通訊錄範例應用程式，您必須符合下列軟體和資料庫需求：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="software-requirements"></a>軟體需求  
 執行此 Web 應用程式的伺服器電腦軟體需求包括：  
  
-   Microsoft Windows NT® Server 4.0、Service Pack 3 或更新版本，或 Microsoft Windows®2000伺服器。  
  
-   Microsoft Internet Information Services （IIS）3.0 版或更新版本，以及 Active Server Pages。  
  
 執行此 Web 應用程式的用戶端電腦軟體需求包括：  
  
-   Microsoft Internet Explorer 4.0 或更新版本。  
  
-   Microsoft Windows NT 4.0 工作站或伺服器、Windows 2000 或 Microsoft Windows 98。  
  
## <a name="database-requirements"></a>資料庫需求  
 若要使用此範例，您必須具有：  
  
-   可操作的 Microsoft® SQL Server 6.5 版或更新版本的資料庫伺服器。  
  
-   建立資料庫並在其中填入範例資料的許可權。  
  
-   透過 Enterprise Manager 或 ISQL 公用程式（在 SQL Server 7.0 中稱為 Query Analyzer）來驗證填入的資料。  
  
 如果您沒有許可權，您的資料庫管理員可能需要設定系統，並授與您資料庫的存取權限，或為您設定資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [執行通訊錄 SQL 腳本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl 物件（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [執行通訊錄應用程式範例](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


