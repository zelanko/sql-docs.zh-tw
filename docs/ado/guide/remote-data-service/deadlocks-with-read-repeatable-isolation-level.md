---
title: 具有讀取可重複隔離等級的鎖死 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: rothja
ms.author: jroth
ms.openlocfilehash: 31c90281860473d43e0a6bde4d1dd9e64e39bb3f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749640"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>讀取可重複的隔離等級發生死結
如果自訂商務物件使用可重複讀取的隔離等級來存取 SQL Server，而且在相同交易中傳送查詢和更新的兩個用戶端同時呼叫商務物件，則可能會發生鎖死。 遠端資料服務的設計目的是要讓其中一個處理常式釋放鎖死，但該用戶端的更新將會失敗。  
  
 使用[Cursor 服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)**命令逾時**動態屬性來修改超時時間長度。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)



