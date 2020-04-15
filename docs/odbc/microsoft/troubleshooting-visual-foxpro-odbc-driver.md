---
title: 故障排除(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b035069c0be88d05a3aa5e17b96af991c27405
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303029"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑難排解 (Visual FoxPro ODBC Driver)
以下各節討論如何提高性能和解決您在使用 Visual FoxPro ODBC 驅動程式時可能遇到的問題。  
  
## <a name="accessing-parameterized-views"></a>存取參數化檢視  
 無法使用驅動程式訪問 Visual FoxPro 資料庫中的參數化檢視。 參數化檢視在檢視的 SQL **SELECT**語句中創建 WHERE 子句,該語句將下載的記錄限制為滿足使用為參數提供的值生成的 WHERE 子句的條件的記錄。 由於驅動程式不支援將參數傳遞到檢視,因此使用驅動程式訪問參數化視圖的嘗試將失敗。  
  
 參數值可以在運行時提供,也可以以程式設計方式傳遞到檢視。  
  
## <a name="accessing-remote-views"></a>存取遠端檢視  
 無法使用驅動程式存取 Visual FoxPro 資料庫中的遠端檢視。 遠端檢視是存取非 FoxPro 資料或 FoxPro 和非 FoxPro 資料組合的檢視。 要造訪遠端檢視,請使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>刪除記錄  
 您可以使用驅動程式標記記錄以進行刪除,但不能從資料庫中永久刪除記錄。 要從表中永久刪除記錄,請使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>使用後臺擷取提高性能  
 您可以使用驅動程式的背景提取功能提高大型提取的性能。 後台提取使用單獨的線程從特定數據源獲取請求的數據。  
  
 您可以透過以下方式之一對資料來源使用後臺提取:  
  
-   選中[ODBC 視覺化 FoxPro 設定對話框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)上的**後台複選方塊中的「提取資料**」 。  
  
-   在連接字串中使用背景提取屬性關鍵字。  
  
 有關連接字串屬性關鍵字的資訊,請參閱[使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多層檢視  
 多層檢視是基於一個或多個視圖而不是基表的檢視。 更新多層檢視中的數據時,更新只會向下到頂級視圖所基於的視圖,更新只會向下。基表不會更新。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在儲存過程中使用資料定義語言 (DDL)  
 在 Visual FoxPro 儲存過程中,不能使用 DDL,例如建立表或 ALTER TABLE。  
  
 有關可在儲存過程中使用的語言的資訊,請參閱[支援規則、觸發器、預設值和儲存過程](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位更新  
 驅動程式不支援定位更新。 使用 SQL WHERE 子句標識要更新的行。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 開發人員,您應該注意,SET ANSI 的預設設定是驅動程式的「打開」,這與 Visual FoxPro 的預設設定 OFF 相反。 SET ANSI 的預設設定允許 Visual FoxPro 資料源與其他通常執行精確比較的 ODBC 資料來源保持一致。 您可以更改預設設定。 有關詳細資訊,請參閱[SET ANSI](../../odbc/microsoft/set-ansi-command.md)。
