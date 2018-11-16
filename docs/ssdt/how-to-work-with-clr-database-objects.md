---
title: 如何：使用 CLR 資料庫物件 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.allowsqlclrdebugging
ms.assetid: 4a28d43d-eb5e-444d-aace-5df691f38709
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f339b8c73a2bed5a36f61fd1afea7f01afc433dc
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659118"
---
# <a name="how-to-work-with-clr-database-objects"></a>如何：使用 CLR 資料庫物件
除了使用 Transact\-SQL 程式語言以外，還可以使用 .NET Framework 語言來建立擷取及更新資料的資料庫物件。 以受控碼撰寫的資料庫物件稱為 SQL Server Common Language Runtime (CLR) 資料庫物件。 如需使用 SQL Server 中裝載的 CLR 資料庫物件之優點的說明，以及如何在 Transact\-SQL 與 CLR 之間擇一使用，請參閱 [CLR 整合的優點](../relational-databases/clr-integration/clr-integration-overview.md)和[使用受控碼來建立資料庫物件的優點](https://msdn.microsoft.com/library/k2e1fb36.aspx) \(機器翻譯\)。  
  
若要使用 SQL Server Data Tools 建立 CLR 資料庫物件，您可以建立一個資料庫專案，然後在其中加入 CLR 資料庫物件。 不同於舊版 Visual Studio，您不必建立個別的 CLR 專案，再從資料庫專案加入其參考。 建置和發行資料庫專案時，會同時自動發行專案中的 CLR 物件。 這些 CLR 物件發行後，它們可以被呼叫和執行，就像任何其他資料庫物件一樣。  
  
[CLR] 和 [CLR 建置] 屬性頁包含許多在專案中使用 CLR 資料庫物件的設定。 具體來說，[CLR] 屬性頁含有權限等級設定，可設定對 CLR 組件的權限。 它還擁有 [產生 DDL] 設定，可以控制是否要產生已加入專案中之 CLR 資料庫物件的 DDL。 [CLR 建置] 屬性頁包含所有的編譯器選項，可用來設定專案中 CLR 程式碼的編譯組態。 您可以存取這些屬性頁，方法是以滑鼠右鍵按一下 [方案總管] 中的專案，再選取 [屬性]。  
  
若要啟用 CLR 資料庫物件偵錯，請開啟 [SQL Server 物件總管]。 以滑鼠右鍵按一下含有您要偵錯之 CLR 資料庫成品的伺服器，然後選擇 [允許 SQL/CLR 偵錯]。 訊息方塊隨即出現，其中會顯示警告：「請注意，當偵錯時，此伺服器上的所有 Managed 執行緒都將停止。 是否要在此伺服器上啟用 SQL CLR 偵錯？」。 當您對 CLR 資料庫物件進行偵錯時，中斷執行就會中斷伺服器上的所有執行緒，並影響其他使用者。 因此，您不應在實際執行伺服器上偵錯 CLR 資料庫物件的應用程式。 您也應注意，一旦啟動偵錯之後，就無法再變更 [SQL Server 物件總管] 中的設定。 啟動下一個偵錯工作階段前，在 [SQL Server 物件總管] 中進行的變更不會生效。  
  
如需有關建置 CLR 資料庫物件之需求的詳細資訊，請參閱[利用 Common Language Runtime (CLR) 整合建立資料庫物件](https://msdn.microsoft.com/library/ms131046.aspx)。  
  
> [!WARNING]  
> 下列程序使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-add-a-clr-database-object-to-your-project"></a>若要將 CLR 資料庫物件加入專案中  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 資料庫專案，再依序選取 [加入] 和 [新增項目]。  
  
2.  依序選取 [C# SQL CLR] 範本和 [SQL CLR 使用者定義函式]。 接受預設名稱，並按一下 [加入]。  
  
3.  將下列程式碼加入類別主體中。 這個函式會驗證美國電話號碼。 它必須由選擇性以括號括住的 3 個數字字元，後面接著一組 3 個數字字元再接著一組 4 個數字字元組成。 支援的格式範例有 (425) 555-0123、425-555-0123、425 555 0123 和 1-425-555-0123。  
  
    ```  
  
    [SqlFunction(IsDeterministic = true, IsPrecise = true)]  
    public static SqlBoolean validatePhone(SqlString phone)  
    {  
        string aNorthAmericanPhoneNumberPattern = @"^[01]?[- .]?(\([2-9]\d{2}\)|[2-9]\d{2})[- .]?\d{3}[- .]?\d{4}$";  
        if (!phone.IsNull)  
        {  
           Regex regex = new Regex(aNorthAmericanPhoneNumberPattern);  
           return regex.IsMatch(phone.Value);  
        }  
        return true;  
     }  
    ```  
  
4.  請注意，`Regex` 是以紅色加上底線標示的文字。 以滑鼠右鍵按一下 `Regex`，再依序選取 [解析] 和 [使用 System.Text.RegularExpressions]。  
  
5.  如果是針對 Microsoft SQL Server 2012 伺服器執行個體進行開發，則可以略過這個步驟。 否則，SQL Server 2005 和 SQL Server 2008 只支援使用 .NET Framework 2.0、3.0 或 3.5 版本建置的資料庫專案。 若要確定 .NET 目標平台是否設定正確，請以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 資料庫專案，再選取 [屬性]。 在 [SQLCLR] 屬性頁中，將 [目標平台] 變更為 [.NET Framework 3.5] 或以下版本。 按一下最後一個畫面中的 [是] 以關閉並重新開啟專案。  
  
6.  以滑鼠右鍵按一下 [TradeDev] 專案，再選取 [建置] 建置專案。  
  
7.  按兩下 Suppliers.sql 並選取 [檢視表設計工具]，在資料表設計工具中開啟 Suppliers 資料表。  
  
8.  在資料行格線中按一下空的資料列，將新的資料列加入資料表中。 分別為 [名稱] 和 [資料類型] 欄位輸入 **phone** 和 **nvarchar (128)**，並保持 [允許 Null] 欄位處於選取狀態。  
  
9. 以滑鼠右鍵按一下內容窗格中的 [檢查條件約束] 節點，再選取 [加入新的檢查條件約束]。  
  
10. 以下列內容取代指令碼窗格中之條件約束的預設定義。  
  
    ```  
    CONSTRAINT [CK_Suppliers_CheckPhone] CHECK (dbo.validatePhone(phone)=1),  
    ```  
  
    這樣可以確保會使用先前加入的 CLR UDF 檢查對新電話號碼欄位的任何輸入。  
  
11. 按 F5 建置並部署專案至本機資料庫。  
  
### <a name="to-use-clr-database-objects"></a>若要使用 CLR 資料庫物件  
  
1.  在 [SQL Server 物件總管] 中，巡覽至專案部署目標位置的本機資料庫。  
  
2.  預設會關閉 SQL Server 中的 CLR 整合功能。 您必須啟用 CLR 整合，才能使用 CLR 資料庫物件。 若要這麼做，請使用 sp_configure 預存程序的 "clr enabled" 選項。 如需詳細資訊，請參閱 [clr enabled 選項主題](../relational-databases/clr-integration/clr-integration-enabling.md)。  
  
    以滑鼠右鍵按一下資料庫，再選取 [新增查詢]。 在查詢窗格中，貼上下列程式碼，再按 [執行查詢] 按鈕。  
  
    ```  
  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO  
    ```  
  
3.  以滑鼠右鍵按一下 [Suppliers] 資料表，再選取 [檢視資料]。  
  
4.  分別為 [id]、[name] 和 [phone] 輸入 **5**、**Contoso** 和 **425 3122 1222**，並保持 [Address] 欄位空白。 按 TAB 離開 [phone] 欄位，並留意到快顯的訊息指出 `INSERT` 陳述式與現有的檢查條件約束 (使用預先定義的電話號碼模式檢查對 [phone] 欄位的輸入) 相衝突。  
  
5.  將輸入變更為 **425 312 1222**，再按 TAB 鍵離開。 請注意，這一次的輸入被接受。  
  
## <a name="see-also"></a>另請參閱  
[CLR 整合的優點](../relational-databases/clr-integration/clr-integration-overview.md) \(機器翻譯\)  
[使用受控碼來建立資料庫物件的優點](https://msdn.microsoft.com/library/k2e1fb36.aspx) \(機器翻譯\)  
[利用 Common Language Runtime (CLR) 整合組建資料庫物件](https://msdn.microsoft.com/library/ms131046.aspx)  
  
