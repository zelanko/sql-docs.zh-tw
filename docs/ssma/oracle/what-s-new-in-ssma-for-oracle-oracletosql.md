---
title: "什麼 &#39; s SSMA for Oracle (OracleToSQL) 的新功能 |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 191fe2e11c43f4c190a87ee52df9ff87c259ea7d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-oracle-oracletosql"></a>什麼 &#39; s SSMA for Oracle (OracleToSQL) 的新功能
本主題列出每個版本中的 Oracle 變更 SSMA。  

## <a name="may-2016"></a>2016 年  
2016 年版本的 SSMA for Oracle 包含下列變更：  

1.  已新增的支援 SQL Server 2016
2.  新增的轉換 Oracle 回溯封存資料表為時態表的 SQL Server
3.  加入的轉換的 Oracle VPD 原則轉換成 SQL Server 原則物件 （Oracle 的資料列層級安全性）
4.  初始載入 oracle 降低的時間
5.  改良的剖析和解析程式
6.  移除.Net 2.0 的安裝程式檢查
7.  更新延伸模組組件相依於.Net 3.5.Net 4.0
8.  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令
9.  SSMA 主控台的固定"securepassword 」 命令
10. 固定的初始載入的物件計數
11. 固定轉換字元資料類型的 for Oracle
12. 通用設定 中修正的 bug
  
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for Oracle 包含下列變更：  
  
1.  支援移轉至 SQL Server 2016  
  
2.  支援移轉 Oracle 的資料列層級安全性 （有限制）  
  
3.  支援移轉的記憶體中的 Oracle 資料表中，以 SQL Server 資料行存放區  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月維護版的 SSMA for Oracle 包含下列變更：  
  
1.  加入叢集索引的支援  
  
2.  固定慢速 Oracle 結構描述查詢 (RFC 5076207)  
  
3.  固定從主控台連線至 Azure  
  
4.  加入的檢視記錄檔功能表項目 SSMA (建議 RFC 5706203)  
  
5.  加入的遙測  
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版本的 SSMA for Oracle 包含下列變更：  
  
1.  Azure SQL 資料庫的支援  
  
2.  移至結構描述，以支援 Azure SQL DB 的延伸模組組件功能  
  
3.  支援的 Oracle 具體化檢視  
  
4.  支援 SQL Server 2014 記憶體最佳化資料表  
  
5.  測試針對具有超過 10k 的資料庫物件的效能改進  
  
6.  處理大量物件的 UI 增強功能  
  
7.  反白顯示的 「 已知 」 的 LOB 結構描述  
  
8.  轉換速度改善  
  
9. 顯示在 UI 中的物件計數  
  
10. 報表大小縮減超過 25%  
  
11. 未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
2014 年 4 月發行的 SSMA for Oracle 包含下列變更：  
  
1.  已新增的支援 MS SQL Server 2014。  
  
2.  已新增的支援 Oracle 12 和查詢的最佳化。  
  
3.  關於 Azure 的轉換已經修正的 bug。  
  
4.  關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
2012 年 1 月版本的 SSMA for Oracle 包含下列變更：  
  
-   支援資料列型別和 RecordType 輸入的參數預設為 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版本的 SSMA for Oracle 包含下列變更：  
  
-   支援的 Oracle 順序轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"順序產生器。  
  
-   在資料遷移期間報告改良的錯誤。  
  
-   改進的轉換的陳述式使用保留的字。  
  
-   改善的函式中的日期值的隱含轉換。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月發行的 SSMA for Oracle 包含下列變更：  
  
-   彙總支援的"SSMA for Oracle"產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   連接及移轉至支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   增強用戶端資料移轉的引擎，支援平行的資料移轉。  
  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
  
-   較早版本的 SSMA （v4.0 和 4.2 版） 所建立之專案的回溯相容性。  
  
-   SSMA for Oracle v5.0 產品可以安裝與舊版本的 SSMA （v4.0 和 4.2 版） 的並存 (SxS)。  
  
-   報告 （包括子類型、 VARRAY、 巢狀資料表、 物件資料表和物件檢視） 的使用者定義類型和其 PL/SQL 區塊使用特殊的錯誤訊息中的使用方式的支援。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Oracle 的 2010 年 7 月發行版本包含下列變更：  
  
-   移轉至 SQL Server 2008 R2 的支援  
  
-   命令列執行新的 SSMA 主控台應用程式  
  
-   使用伺服器端和用戶端端資料移轉引擎的資料移轉支援  
  
-   「 自訂選取 」 陳述式中的資料移轉支援  
  
-   支援從 Oracle 11g R2 移轉  
  
## <a name="june-2008"></a>2008 年 6 月  
2008 年 6 月版本的 SSMA for Oracle 包含下列變更：  
  
-   已完成評估報表中的增強功能。 它包含同義字的其他資訊、 剖析物件、 面板和 SQL Server 標誌移除，和配置保存的未經處理資料來源。  
  
-   在物件轉換中的增強功能：  
  
    -   套件 DBMS_LOB、 加入 DBMS_SQL 轉換。  
  
    -   聯結修訂的轉換。  
  
    -   集合和記錄轉換，現在在簡單案例中透過不同的變數，每個欄位發行記錄轉換的修改。  
  
    -   改進的記錄和集合的實作。  
  
    -   視窗型彙總函式加入。  
  
    -   新增彙總套件/CUBE 子句。  
  
    -   NEXTVAL/CURVAL 的改進。  
  
    -   在 SET 子句中群組資料行，已加入群組集合及群組識別碼。  
  
    -   MERGE 陳述式加入。  
  
    -   新的日期時間類型和 CLR 資料型別加入記錄和集合轉換支援。  
  
-   已加入的測試人員的新功能。 資料表現在可以測試以使用 Tester 物件、 測試案例中的數個可測試物件的呼叫順序可以改變、 使用者可以測試程序和函式與記錄和做為參數的集合，並將傳回值，而加入分析器檢查相依性只使用資料表。  
  
## <a name="august-2007"></a>2007 年 8 月  
2007 年 8 月版本的 SSMA for Oracle 包含下列變更：  
  
-   新的測試人員元件可讓您建立、 管理及執行測試案例，以確認已轉換的 SQL 程式碼。  
  
-   轉換的 Oracle 子型別、 集合和本機模組已新增至 SQL 轉換器。  
  
-   新的同步處理功能可讓您同步處理與 SQL Server 資料庫的特定物件。  
  
-   加入新的轉換選項。  
  
## <a name="april-2007"></a>2007 年 4 月  
2007 年 4 月版的 SSMA for Oracle 是最早的版本。  
  

