---
title: "執行活頁簿 SQL 指令碼 |Microsoft 文件"
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
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ab669066b0440807a4a2475817e0dbda047cb79
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="running-the-address-book-sql-script"></a>執行活頁簿 SQL 指令碼
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 您必須使用 ISQL/Query Analyzer 的命令列公用程式或 SQL Server Enterprise Manager 來執行包含的 SQL 指令碼 (Sampleemp.sql):  
  
-   建立新的資料庫，AddrBookDB，預設的裝置上。  
  
-   連接到資料庫，AddrBookDB。  
  
-   建立員工資料表。  
  
-   於其中填入範例資料的資料表。  
  
-   執行簡單的 SELECT 陳述式，以確認資料庫資料表的母體擴展。  
  
-   設定名為"adcdemo 」 與 「 adcdemo。 」 的密碼的使用者帳戶  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>若要執行 Microsoft SQL Server 6.5 Sampleemp.sql 指令碼  
  
1.  按一下**啟動**，指向 **程式**，然後指向**Microsoft SQL Server 6.5**。 按一下**SQL Enterprise Manager**。  
  
2.  從**工具**功能表上，按一下  **SQL 查詢工具**。  
  
3.  按一下**負載 SQL 指令碼**並瀏覽至 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
4.  選取 Sampleemp.sql 的檔案。 按一下 **[開啟]**。  
  
5.  按一下**執行查詢**按鈕 （工具列上的綠色箭頭）。  
  
6.  它會執行之後，請關閉**查詢**和**Enterprise Manager** windows。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>若要執行 Microsoft SQL Server 7.0 Sampleemp.sql 指令碼  
  
1.  按一下**啟動**，指向 **程式**，然後指向**Microsoft SQL Server 7.0**。 按一下**Enterprise Manager**。  
  
2.  請確定您從已註冊的伺服器在 Enterprise Manager 中的程式清單中選取您想要使用 SQL Server。  
  
3.  從**工具**功能表上，按一下  **SQL Server Query Analyzer**。  
  
4.  按一下**負載 SQL 指令碼**按鈕 （工具列上開啟的資料夾），瀏覽至 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
5.  選取 Sampleemp.sql 的檔案。 按一下 **[開啟]**。  
  
6.  按一下**執行查詢**按鈕 （工具列上的綠色箭頭） 或**F5**。  
  
7.  它會執行之後，請關閉**查詢**， **Query Analyzer**，和**Enterprise Manager** windows。  
  
## <a name="see-also"></a>請參閱＜  
 [執行通訊錄範例應用程式](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


