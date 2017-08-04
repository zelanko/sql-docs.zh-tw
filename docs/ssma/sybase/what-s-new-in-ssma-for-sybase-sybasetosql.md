---
title: "什麼 &#39; s SSMA for Sybase (SybaseToSQL) 的新功能 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d97e03212e6985ce9d506774bfff0aa2f4ec8d1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>什麼 &#39; s SSMA for Sybase (SybaseToSQL) 的新功能
本主題列出 SSMA for Sybase 變更每個版本中。  

## <a name="may-2016"></a>2016 年  
2016 年版的 SSMA for Sybase 包含下列變更：  

1.  已新增的支援 SQL Server 2016
2.  移除.Net 2.0 的安裝程式檢查
3.  更新延伸模組組件相依於.Net 3.5.Net 4.0
4.  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令
5.  SSMA 主控台的固定"securepassword 」 命令
6.  固定的初始載入的物件計數
7.  通用設定 中修正的 bug

## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月 preview 版的 SSMA for Sybase 包含下列變更：  
  
1.  支援移轉至 SQL Server 2016  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for Sybase 包含下列變更：  
  
1.  加入的檢視記錄檔功能表項目 SSMA (建議 RFC 5706203)  
  
2.  加入的遙測  
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
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
2014 年 4 月版的 SSMA for Sybase 包含下列變更：  
  
-   已新增的支援 MS SQL Server 2014。  
  
-   已修正的 bug，關於轉換至 Azure  
  
-   關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
2012 年 1 月版的 SSMA for Sybase 包含下列變更：  
  
-   回復觸發程序轉換支援。  
  
-   轉換提供修正@ROWCOUNT和 @@ERROR相同的 SET 陳述式。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
-   在資料遷移期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月版的 SSMA for Sybase 包含下列變更：  
  
-   彙總支援的"SSMA for Sybase"產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"與 SQL Azure。  
  
-   連接及移轉至支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
  
-   轉換，並將 Sybase 資料庫移轉到 SQL Azure 的新功能。  
  
-   增強用戶端資料移轉的引擎，支援平行的資料移轉。  
  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
  
-   區分大小寫的 Sybase 資料庫可以正確轉換並移轉至區分大小寫的 SQL Server。  
  
-   支援的 SQL Server ANSI 聯結陳述式 Sybase ASE 非 ANSI 聯結陳述式的轉換已經擴充成刪除及 UPDATE 陳述式。  
  
-   其他連接選項連接到 Sybase ASE 伺服器使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.Net 提供者。  
  
-   移除個別的資料庫上的相依性呼叫**SysDB**包含 Sybase 模擬函式 （做為延伸模組組件的一部分安裝）。  
  
-   SSMA for Sybase 擴充套件現在可以安裝在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]叢集。  
  
-   較早版本的 SSMA （v4.0 和 4.2 版） 所建立之專案的回溯相容性。  
  
-   SSMA for Sybase v5.0 產品可以安裝與舊版本的 SSMA （v4.0 和 4.2 版） 的並存 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
2010 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
-   移轉至 SQL Server 2008 R2 的支援  
  
-   命令列執行新的 SSMA 主控台應用程式  
  
-   使用伺服器端和用戶端端資料移轉引擎的資料移轉支援  
  
-   「 自訂選取 」 陳述式中的資料移轉支援  
  
-   從 Sybase ASE 15.0.3 和 15.5 移轉的支援  
  
## <a name="june-2008"></a>2008 年 6 月  
2008 年 6 月版的 SSMA for Sybase 包含下列變更：  
  
-   SSMA Tester 加入，它會自動測試轉換資料庫物件和所做的 SSMA 資料移轉。 所有 SSMA 的移轉步驟都完成之後，請確認已轉換的物件運作的方式相同，而且已正確地傳送的所有資料使用 SSMA 軟體測試人員。  
  
-   加入的每個 SQL 轉換。 使用者現在可以指定暫存資料表 （和其他物件） 來轉換中每個來源程序的宣告。  
  
-   在物件轉換中的增強功能：  
  
    -   聯結修訂的轉換。  
  
    -   彙總和非彙總而不需/群組 by 子句。  
  
    -   IDENTITY 函式使用 SELECT INTO 陳述式。  
  
    -   叢集條件約束和索引上的資料僅鎖定。  
  
    -   SELECT INTO 所建立的暫存資料表。  
  
    -   條件約束 / 索引的暫存資料表。  
  
    -   新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年日期時間類型支援。  
  
    -   Sybase 15.0 連線和資料類型的支援。  
  
## <a name="may-2007"></a>May 2007  
May 2007 版的 SSMA for Sybase 包含下列變更：  
  
-   當您儲存專案時，載入資料庫內容的速度。  
  
-   支援的 SQL Server 格式化 SQL 模式的使用者輸入註解。  
  
-   在物件轉換中的增強功能。  
  
請注意此版本未更新的說明檔。 如需詳細資訊，請參閱本主題稍後的文件集注意事項 > 一節。  
  
## <a name="november-2006"></a>2006 年 11 月  
2006 年 11 月版的 SSMA for Sybase 包含下列變更：  
  
-   新的通用設定：  
  
    -   您可以選擇在編輯器視窗中顯示行號。  
  
    -   您可以設定 SSMA 提示來取代重複的物件，或一律或永遠不會取代重複的物件結構描述轉換期間。  
  
-   新的轉換選項可讓您設定 SSMA 如何處理在下列情況：  
  
    -   包含二進位字串的 CAST 或 CONVERT 陳述式  
  
    -   檢查相等運算式中的 null 值  
  
    -   Proxy 資料表  
  
    -   Raiserror 的使用者訊息錯誤號碼  
  
    -   包含無法解析識別項的 UPDATE 陳述式  
  
-   新的移轉選項可讓您指定 SSMA 應該如何處理外的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]日期範圍。  
  
-   A**格式化 SQL**上設定**SQL**索引標籤上，將格式化的程式碼，以改善可讀性。  
  
-   Bug 修正，包括：  
  
    -   SSMA 現在將轉換鎖定資料表*資料表*IN {共用 |TABLOCK 或 TABLOCKX 提示加入後續的 SELECT 查詢，在資料表上的獨佔} 模式陳述式。  
  
    -   在字元運算式中使用二進位類型時，現在會加入必要的轉型。  
  
    -   記憶體和效能增強功能。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月版的 SSMA for Sybase 是最早的版本。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

