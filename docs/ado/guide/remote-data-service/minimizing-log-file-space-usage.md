---
title: 記錄檔空間使用量降到最低 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- log file space in RDS [ADO]
ms.assetid: 669662a0-e20f-483e-ab28-53f66c524c98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 061cae6b387611886943aabcfa3dfd99579a59d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134393"
---
# <a name="minimizing-log-file-space-usage"></a>將記錄檔空間使用量降到最低
記錄檔可能會迅速填滿 （因此暫停伺服器） 如果有大型的磁碟區上的 SQL Server 資料庫的活動。 您可以將記錄檔設定為**檢查點截斷**大幅擴充的資料庫記錄檔的生命週期。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>若要啟用 Microsoft SQL Server 6.5 中的檢查點截斷  
  
1.  啟動 Microsoft SQL Server Enterprise Manager、 開啟樹狀結構的伺服器，然後再開啟資料庫裝置的樹狀結構。  
  
2.  按兩下要啟用這項功能的資料庫名稱。  
  
3.  從**資料庫**索引標籤上，選取**Truncate**。  
  
4.  從**選項**索引標籤上，選取**檢查點截斷記錄檔**，然後按一下**確定**。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>若要啟用 Microsoft SQL Server 7.0 中的檢查點截斷  
  
1.  啟動 Microsoft SQL Server Enterprise Manager、 開啟樹狀結構的伺服器，然後再開啟資料庫樹狀結構。  
  
2.  這項功能將會啟用並選擇在其的資料庫名稱上按一下滑鼠右鍵**屬性**。  
  
3.  從**選項**索引標籤上，選取**檢查點截斷記錄檔**，然後按一下**確定**。  
  
 如需詳細資訊**檢查點截斷**功能，請參閱 Microsoft SQL Server 文件。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


