---
title: 執行通訊錄 SQL 腳本 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5adc631a3c3f7a66c02f9ebfe541fa5e923deb0a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922233"
---
# <a name="running-the-address-book-sql-script"></a>執行通訊錄 SQL 指令碼
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 您必須使用 ISQL/Query Analyzer 命令列公用程式或 SQL Server Enterprise Manager 來執行內含的 SQL 腳本（Sampleemp），其：  
  
-   在預設裝置上建立新的資料庫 AddrBookDB。  
  
-   連接到資料庫（AddrBookDB）。  
  
-   建立 Employee 資料表。  
  
-   在資料表中填入範例資料。  
  
-   執行簡單的 SELECT 語句，以驗證資料庫資料表的填入。  
  
-   設定名為 "adcdemo" 且密碼為 "adcdemo" 的使用者帳戶。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>若要在 Microsoft SQL Server 6.5 中執行 Sampleemp 腳本  
  
1.  按一下 [**開始**]，指向 [**程式**]，然後指向 [ **Microsoft SQL Server 6.5**]。 按一下 **[SQL Enterprise Manager**]。  
  
2.  從 [**工具**] 功能表中，按一下 [ **SQL 查詢工具**]。  
  
3.  按一下 [**載入 SQL 腳本**]，然後流覽至 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
4.  選取 Sampleemp 檔案。 按一下 **[開啟]** 。  
  
5.  按一下 [**執行查詢**] 按鈕（工具列上的綠色箭號）。  
  
6.  執行之後，請關閉 [**查詢**] 和 [ **Enterprise Manager** ] 視窗。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>若要在 Microsoft SQL Server 7.0 中執行 Sampleemp 腳本  
  
1.  按一下 [**開始**]，指向 [**程式**]，然後指向 [ **Microsoft SQL Server 7.0**]。 按一下 [ **Enterprise Manager**]。  
  
2.  請確定您要使用的 SQL Server 已從 Enterprise Manager 中已註冊的伺服器清單中選取。  
  
3.  從 [**工具**] 功能表中，按一下 [ **SQL Server Query Analyzer**]。  
  
4.  按一下 [**載入 SQL 腳本**] 按鈕（工具列上的 [開啟] 資料夾），然後流覽至 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
5.  選取 Sampleemp 檔案。 按一下 **[開啟]** 。  
  
6.  按一下 [**執行查詢**] 按鈕（工具列上的綠色箭號）或**F5**。  
  
7.  執行之後，請關閉 [**查詢**]、[**查詢分析器**] 和 [ **Enterprise Manager** ] 視窗。  
  
## <a name="see-also"></a>另請參閱  
 [執行通訊錄應用程式範例](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


