---
description: 將記錄檔空間使用量降到最低
title: 最小化記錄檔空間使用量 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b839f5f31671d7364eeec022da1b25bdf584a3a
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759718"
---
# <a name="minimizing-log-file-space-usage"></a>將記錄檔空間使用量降到最低
記錄檔可能會快速填滿 (因此當 SQL Server 資料庫上有大量的活動時，就會停止伺服器) 。 您可以將記錄檔設定為 **在檢查點截斷** ，以大幅延長資料庫記錄檔的存留期。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-65"></a>在 Microsoft SQL Server 6.5 中啟用檢查點的截斷  
  
1.  啟動 Microsoft SQL Server Enterprise 管理員]，開啟伺服器的樹狀結構，然後開啟 [資料庫裝置] 樹狀目錄。  
  
2.  按兩下將啟用這項功能的資料庫名稱。  
  
3.  在 [ **資料庫** ] 索引標籤中，選取 [ **截斷**]。  
  
4.  在 [ **選項** ] 索引標籤中，選取 [ **截斷檢查點上的記錄**]，然後按一下 **[確定]**。  
  
### <a name="to-enable-truncate-on-checkpoint-in-microsoft-sql-server-70"></a>在 Microsoft SQL Server 7.0 中啟用檢查點的截斷  
  
1.  啟動 Microsoft SQL Server Enterprise 管理員]，開啟伺服器的樹狀結構，然後開啟 [資料庫] 樹狀目錄。  
  
2.  以滑鼠右鍵按一下將啟用這項功能的資料庫名稱，然後選擇 [ **屬性**]。  
  
3.  在 [ **選項** ] 索引標籤中，選取 [ **截斷檢查點上的記錄**]，然後按一下 **[確定]**。  
  
 如需有關「 **截斷于檢查點** 」功能的詳細資訊，請參閱 Microsoft SQL Server 檔。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)