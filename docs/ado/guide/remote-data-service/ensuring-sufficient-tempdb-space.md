---
title: 確保有足夠的 TempDB 空間 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c86196fdf0320b5f3cb5028cb7d5db484c4da846
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ensuring-sufficient-tempdb-space"></a>確保有足夠的 TempDB 空間
如果在處理時所發生的錯誤[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)需要處理在 Microsoft SQL Server 6.5 空間的物件，您可能需要增加 TempDB 的大小。 (某些查詢需要暫存處理空間; 例如，具有 ORDER BY 子句的查詢則需要排序的**資料錄集**，這需要一些暫存空間。)  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!IMPORTANT]
>  閱讀此程序之前執行的動作，因為它不是容易壓縮裝置之後，已展開節點。  
  
> [!NOTE]
>  根據預設 Microsoft SQL Server 7.0 和更新版本、 TempDB 是設定為視需要自動成長。 因此，此程序可能只必須執行版本早於 7.0 的伺服器上。  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>若要增加 SQL Server 6.5 的 TempDB 空間  
  
1.  啟動 Microsoft SQL Server Enterprise Manager，開啟樹狀目錄中的伺服器，並開啟資料庫裝置樹狀結構。  
  
2.  選取 （實體） 的裝置，若要擴充，例如 Master，然後按兩下以開啟裝置**編輯資料庫裝置** 對話方塊。  
  
     這個對話方塊會顯示目前的資料庫正在使用多少空間。  
  
3.  在**大小**方塊中，增加的裝置所需的數量 (例如，50 mb 的硬碟空間)。  
  
4.  按一下**立即變更**增加，可以展開 （邏輯） TempDB 的空間數量。  
  
5.  開啟伺服器上的資料庫樹狀目錄，然後按兩下**TempDB**開啟**編輯資料庫** 對話方塊。 **資料庫**索引標籤會列出目前配置給 TempDB 的空間數量 (**資料大小**)。 根據預設，這會是 2 MB。  
  
6.  在下**大小**群組中，按一下**展開**。 下圖會顯示在每個實體裝置上的可用和已配置的空間。 中 暗紅色色彩的長條表示可用的空間。  
  
7.  選取**記錄裝置**，例如 Master，若要顯示在可用的大小**大小 (MB)** 方塊。  
  
8.  按一下**現在展開**酃 TempDB 資料庫。  
  
     **編輯資料庫**對話方塊會顯示新針對 TempDB 配置大小。  
  
 如需有關本主題的詳細資訊，請搜尋 「 展開資料庫 對話方塊。 」 的 Microsoft SQL Server Enterprise Manager 的說明檔  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


