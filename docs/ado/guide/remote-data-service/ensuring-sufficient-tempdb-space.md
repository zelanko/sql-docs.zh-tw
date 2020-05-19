---
title: 確保有足夠的 TempDB 空間 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
author: rothja
ms.author: jroth
ms.openlocfilehash: a783c6b6cecbd1fb4139d0ffd3af1a960347f968
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749579"
---
# <a name="ensuring-sufficient-tempdb-space"></a>確認 TempDB 有足夠空間
如果在處理需要在 Microsoft SQL Server 6.5 上處理空間的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件時發生錯誤，您可能需要增加 TempDB 的大小。 （有些查詢需要暫時的處理空間; 例如，具有 ORDER BY 子句的查詢需要**記錄集**，這需要一些暫存空間）。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!IMPORTANT]
>  請先閱讀此程式再執行動作，因為它在擴充後並不容易壓縮裝置。  
  
> [!NOTE]
>  根據預設，inMicrosoft SQL Server 7.0 和更新版本，TempDB 會設定為視需要自動成長。 因此，只有在執行7.0 之前版本的伺服器上，才需要執行此程式。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>增加 SQL Server 6.5 上的 TempDB 空間  
  
1.  啟動 Microsoft SQL Server Enterprise 管理員]，開啟伺服器的樹狀目錄，然後開啟 [資料庫裝置] 樹狀目錄。  
  
2.  選取要展開的（實體）裝置（例如 [主機]），然後按兩下裝置以開啟 [**編輯資料庫裝置**] 對話方塊。  
  
     這個對話方塊會顯示目前的資料庫正在使用多少空間。  
  
3.  在 [**大小**] 方塊中，將裝置增加到所需的數量（例如，硬碟空間 50 mb）。  
  
4.  按一下 [**立即變更**]，以增加（邏輯） TempDB 可以展開的空間量。  
  
5.  開啟伺服器上的 [資料庫] 樹狀結構，然後按兩下 [ **TempDB** ] 以開啟 [**編輯資料庫**] 對話方塊。 [**資料庫**] 索引標籤會列出目前配置給 TempDB 的空間量（**資料大小**）。 此值預設為 2 MB。  
  
6.  在 [**大小**] 群組底下，按一下 [**展開**]。 圖表會顯示每個實體裝置上可用和已配置的空間。 以褐紫紅色色彩表示可用空間。  
  
7.  選取**記錄裝置**（例如 Master）以顯示 [**大小（MB）** ] 方塊中的可用大小。  
  
8.  按一下 [**立即展開**]，將該空間配置給 TempDB 資料庫。  
  
     [**編輯資料庫**] 對話方塊會顯示 TempDB 的新配置大小。  
  
 如需有關此主題的詳細資訊，請在 Microsoft SQL Server Enterprise 管理員說明檔中，搜尋 [展開資料庫] 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


