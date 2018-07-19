---
title: 疑難排解 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23bab07c1f00abc9fb0d2c353603a21b58975933
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905366"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>疑難排解 （Visual FoxPro ODBC 驅動程式）
下列各節討論如何改善效能，並解決使用 Visual FoxPro ODBC 驅動程式時可能會遇到的問題。  
  
## <a name="accessing-parameterized-views"></a>存取參數化的檢視  
 您無法存取 Visual FoxPro 資料庫使用驅動程式中的參數化的檢視。 參數化的檢視建立 WHERE 子句在檢視的 SQL**選取**陳述式來限制記錄下載到符合所提供的值使用的參數建立的 WHERE 子句條件的記錄。 驅動程式不支援將參數傳遞至檢視，因為嘗試存取的參數化的檢視使用驅動程式將會失敗。  
  
 可以在執行階段提供參數值，或以程式設計的方式傳遞到檢視。  
  
## <a name="accessing-remote-views"></a>存取遠端檢視  
 您無法存取遠端 Visual FoxPro 資料庫使用驅動程式中的檢視。 遠端檢視是存取非 FoxPro 資料或 FoxPro 和非 FoxPro 資料的組合。 若要存取遠端的檢視，請使用 Visual FoxPro。  
  
## <a name="deleting-records"></a>刪除資料錄  
 您可以使用驅動程式，刪除的記錄，但您永久無法從資料庫移除記錄。 若要永久移除資料表的記錄，請使用 Visual FoxPro。  
  
## <a name="increasing-performance-using-background-fetching"></a>提高效能使用背景擷取  
 您可以利用擷取功能的驅動程式的背景，以改善效能大的提取上。 背景擷取會在另一個執行緒使用來提取要求特定資料來源的資料。  
  
 您可以採用下列方式之一為資料來源擷取的背景：  
  
-   檢查**提取資料，在背景中的**上的核取方塊[ODBC Visual FoxPro 安裝程式對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)。  
  
-   在連接字串中使用 BackgroundFetch 屬性關鍵字。  
  
 如需連接字串屬性關鍵字資訊，請參閱[使用連接字串](../../odbc/microsoft/using-connection-strings.md)。  
  
## <a name="updating-multitiered-views"></a>更新多層式檢視  
 多層式檢視是根據一個或多個檢視而非基底資料表的檢視。 當您更新多層式檢視中的資料時，更新往只有一個層級，的檢視在最上層檢視基礎;基底資料表不會更新。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>在預存程序中使用資料定義語言 (DDL)  
 Visual FoxPro 預存程序中，您無法使用 DDL，例如 CREATE TABLE 或 ALTER TABLE。  
  
 如需您可以使用預存程序中的語言資訊，請參閱[規則、 觸發程序，預設值和預存程序支援](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)。  
  
## <a name="using-positioned-updates"></a>使用定位的更新  
 驅動程式不支援定位的更新。 您可以使用 SQL WHERE 子句來識別您想要更新的資料列。  
  
## <a name="using-the-set-ansi-command"></a>使用 SET ANSI 命令  
 如果您是 Visual FoxPro 開發人員，您應該注意設定 ANSI 的預設設定是 ON，驅動程式，相較於預設值為 OFF Visual FoxPro。 設定 ANSI 設定上的預設值可讓 Visual FoxPro 資料來源，以便與其他 ODBC 資料來源通常執行精確的比較有一致的行為。 您可以變更預設設定。 如需詳細資訊，請參閱[設定 ANSI](../../odbc/microsoft/set-ansi-command.md)。
