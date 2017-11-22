---
title: "記錄檔空間使用量降到最低 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddb41dbe5a2d76bb26d1830d1b659dbd99ca1c21
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="minimizing-log-file-space-usage"></a>記錄檔空間使用量降到最低
記錄檔可能會迅速填滿 （因此暫停伺服器） 如果有大量的活動上的 SQL Server 資料庫。 您可以將記錄檔設定為**在檢查點截斷**大幅擴充資料庫的記錄檔的存留期。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>若要啟用 Microsoft SQL Server 6.5 中的檢查點截斷  
  
1.  啟動 Microsoft SQL Server Enterprise Manager，開啟樹狀目錄中的伺服器，並開啟資料庫裝置樹狀結構。  
  
2.  按兩下可啟用此功能的資料庫名稱。  
  
3.  從**資料庫**索引標籤上，選取**Truncate**。  
  
4.  從**選項**索引標籤上，選取**檢查點截斷記錄檔**，然後按一下 **確定**。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>若要啟用 Microsoft SQL Server 7.0 中的檢查點截斷  
  
1.  啟動 Microsoft SQL Server Enterprise Manager，開啟樹狀目錄中的伺服器，並開啟資料庫樹狀結構。  
  
2.  以滑鼠右鍵按一下的資料庫的這項功能將會啟用並選擇名稱**屬性**。  
  
3.  從**選項**索引標籤上，選取**檢查點截斷記錄檔**，然後按一下 **確定**。  
  
 如需有關**在檢查點截斷**功能，請參閱 Microsoft SQL Server 文件。  
  
## <a name="see-also"></a>請參閱＜  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


