---
title: "什麼 &#39; s SSMA for MySQL (MySQLToSql) 的新功能 |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 42706f2ce71fc540d8538f9614f1db17b4f70ea7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma-for-mysql-mysqltosql"></a>什麼 &#39; s SSMA for MySQL (MySQLToSql) 的新功能
本主題列出每個版本中的 MySQL 變更 SSMA。  

## <a name="may-2016"></a>2016 年  
SSMA for MySQL 的 2016 年版本包含下列變更:。

1.  已新增的支援 SQL Server 2016
2.  改良的剖析和解析程式
3.  移除.Net 2.0 的安裝程式檢查
4.  更新延伸模組組件相依於.Net 3.5.Net 4.0
5.  固定的預設用於 MySql 的 BigInt typemapping
6.  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令
7.  SSMA 主控台的固定"securepassword 」 命令
8.  固定的初始載入的物件計數
9.  載入的固定的 MsSql 物件
10. 通用設定 中修正的 bug 
 
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月 preview 版的 SSMA for MySQL 包含下列變更：  
  
1.  支援移轉至 SQL Server 2016  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for MySQL 包含下列變更：  
  
1.  加入的檢視記錄檔功能表項目 SSMA (建議 RFC 5706203)  
  
2.  加入的遙測  
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
1.  改善的 Azure SQL DB 程式碼轉換  
  
2.  移至結構描述，以支援 Azure SQL DB 的延伸模組組件功能  
  
3.  測試針對具有超過 10k 的資料庫物件的效能改進  
  
4.  處理大量物件的 UI 增強功能  
  
5.  反白顯示的 「 已知 」 的 LOB 結構描述 （因此可在轉換中予以忽略）  
  
6.  轉換速度改善  
  
7.  顯示在 UI 中的物件計數  
  
8.  報表大小縮減超過 25%  
  
9. 未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
2011 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
1.  已新增的支援 MS SQL Server 2014。  
  
2.  已修正的 bug，關於轉換至 Azure  
  
3.  關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
-   支援的限制，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"的位移。  
  
-   在資料遷移期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月版的 SSMA for MySQL 包含下列變更：  
  
-   單一 「 SSMA for MySQL 的 」，可支援可安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"與 SQL Azure。  
  
-   連線能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   增強用戶端資料移轉的引擎，支援平行的資料移轉。  
  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
  
-   SSMA for MySQL 主控台版本支援回溯相容性。 您可以開啟 SSMA v5.0 稍早的版本所建立的專案。  
  
-   SSMA for MySQL v5.0 產品可以安裝與舊版本的 SSMA 產品的並存 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
2010 年 7 月版的 SSMA for MySQL 包含下列功能：  
  
1.  **使用者介面的增強功能：**  
  
    -   MySQL 資料庫物件的 「 SQL 模式 」 索引標籤  
  
    -   MySQL 資料庫物件的 [設定] 索引標籤  
  
    -   MySQL 資料表的 [資料] 索引標籤  
  
    -   轉換和移轉頁面中的已更新的專案設定  
  
    -   在資料表層級的 [資料移轉設定]  
  
2.  **連接到 MySQL 及 SQL Server 的增強功能：**  
  
    -   在 MySQL 的 SSL 連線  
  
    -   SQL Server 中的加密的連線  
  
3.  **MySQL Metabase Explorer 的增強功能：**  
  
    -   正在載入的所有 MySQL 資料庫物件和其各自的索引標籤。  
  
4.  **物件轉換的增強功能：**  
  
    -   轉換的 MySQL Metabase 物件 – 程序、 函數、 檢視、 觸發程序和陳述式。  
  
    -   在資料表中的空間資料類型的有限的支援。  
  
    -   選項可將 MySQL 函式轉換成 SQL Server 預存程序  
  
    -   若要套用 SQL 模式和字元集對應物件轉換期間的選項  
  
5.  **資料移轉的增強功能：**  
  
    -   使用伺服器端和用戶端端資料移轉引擎的資料移轉支援  
  
    -   空間資料移轉支援  
  
    -   自訂 SQL 資料表的資料移轉  
  
6.  **SSMA for MySQL 主控台：**  
  
    -   SSMA for MySQL 針對支援主控台功能  
  
    -   指令碼層級互動的支援  
  
## <a name="january-2010"></a>2010 年 1 月  
2010 年 1 月版的 SSMA for MySQL 是早的版本。 它包含下列功能：  
  
-   若要在內部部署 SQL Server 和 SQL Azure 移轉支援。  
  
-   **功能的快照集：**結構描述和資料移轉的 MySQL 資料表/索引/條件約束。  
  

