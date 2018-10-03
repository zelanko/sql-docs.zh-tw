---
title: 疑難排解 (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f0576d017068b8ab0694da798c5be458f115e56
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667962"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑難排解 (Visual FoxPro ODBC Driver)
下列各節討論如何改善效能，並解決使用 Visual FoxPro ODBC Driver 時可能會遇到的問題。  
  
## <a name="accessing-parameterized-views"></a>存取參數化的檢視  
 您無法存取 Visual FoxPro 資料庫使用的驅動程式中的參數化的檢視。 參數化的檢視中檢視的 SQL 建立 WHERE 子句**選取**陳述式來限制記錄下載到符合條件的 WHERE 子句的參數使用所提供的值來建置這些記錄。 因為驅動程式不支援將參數傳遞至檢視，嘗試存取的參數化的檢視使用驅動程式將會失敗。  
  
 可以在執行階段提供參數值，或以程式設計的方式傳遞至檢視。  
  
## <a name="accessing-remote-views"></a>存取遠端檢視  
 您無法存取 Visual FoxPro 資料庫使用的驅動程式中的遠端檢視。 遠端檢視表是存取非 FoxPro 資料或 FoxPro 和非 FoxPro 資料的組合。 若要存取遠端檢視，請使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>刪除記錄  
 您可以將標記為要刪除使用的驅動程式的記錄，但您永遠無法從資料庫移除記錄。 若要永久從資料表移除記錄，請使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>使用背景擷取 vm 的效能  
 您可以使用背景擷取功能的驅動程式，以改善效能，大型的提取上。 背景擷取來擷取要求的特定資料來源的資料使用個別的執行緒。  
  
 您可以運用背景擷取的資料來源中的下列方法之一：  
  
-   檢查**提取資料，在背景**核取方塊[ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)。  
  
-   在您的連接字串中使用 BackgroundFetch 屬性關鍵字。  
  
 如需關鍵字的連接字串屬性的資訊，請參閱[使用的連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多層式檢視  
 多層式檢視是根據一或多個檢視，而非基底資料表的檢視。 當您更新多層式檢視中的資料時，更新向下只有一個層級中, 移至在所依據的最上層檢視; 的檢視基底資料表不會更新。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在 預存程序中使用資料定義語言 (DDL)  
 Visual FoxPro 預存程序中，您無法使用 DLL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 如需您可以使用預存程序中的語言資訊，請參閱[的規則、 觸發程序、 預設值和預存程序支援](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位的更新  
 驅動程式不支援定位的更新。 您可以使用 SQL WHERE 子句來識別您想要更新的資料列。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 開發人員，您應該留意設定 ANSI 的預設設定是 ON，驅動程式，相較於預設值為 OFF Visual FoxPro。 設定 ANSI 設定上的預設值可讓 Visual FoxPro 資料來源，以與其他 ODBC 資料來源，通常會執行實際的比較有一致的行為。 您可以變更預設設定。 如需詳細資訊，請參閱 <<c0> [ 設定的 ANSI](../../odbc/microsoft/set-ansi-command.md)。
