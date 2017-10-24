---
title: "系統需求，地址通訊錄應用程式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 070c809c23fcd70c5048e70f61ac74ad4bc7ce4b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-address-book-application"></a>通訊錄應用程式的系統需求
若要設定通訊錄範例應用程式，您必須符合下列軟體和資料庫需求：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="software-requirements"></a>軟體需求  
 執行此 Web 應用程式的伺服器電腦的軟體需求包括：  
  
-   Microsoft Windows NT® Server 4.0 Service Pack 3 或更新版本或 Microsoft Windows® 2000 Server。  
  
-   Microsoft 網際網路資訊服務 (IIS) 版本 3.0 或更新版本，與 Active Server Pages。  
  
 執行此 Web 應用程式的用戶端電腦的軟體需求包括：  
  
-   Microsoft Internet Explorer 4.0 或更新版本。  
  
-   Microsoft Windows NT 4.0 工作站或伺服器、 Windows 2000 或 Microsoft Windows 98。  
  
## <a name="database-requirements"></a>資料庫需求  
 若要使用這個範例中，您必須：  
  
-   操作 Microsoft® SQL Server 6.5 版或更新版本資料庫伺服器。  
  
-   若要建立資料庫，並填入範例資料的權限。  
  
-   透過 Enterprise Manager 或 ISQL 公用程式 (稱為 Query Analyzer 中 SQL Server 7.0) 填入資料的驗證。  
  
 如果您沒有權限，您的資料庫管理員可能需要設定和提供您存取資料庫的權限，或將資料庫設定為您的系統。  
  
## <a name="see-also"></a>另請參閱  
 [執行活頁簿 SQL 指令碼](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [執行通訊錄範例應用程式](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)



